# Diseño de Seguridad

El diseño de seguridad del sistema se estructura en torno a dos mecanismos complementarios: la autenticación de las aplicaciones cliente mediante OAuth2, y un modelo de autorización en capas que garantiza el aislamiento de datos entre los distintos espacios de trabajo (workspaces) del sistema multi-tenant.

## 1. Autenticación mediante OAuth2

El sistema autentica a cada agente de inteligencia artificial (cliente MCP) mediante el protocolo OAuth2, implementado a través de los modelos `MCPApplication` y `MCPAccessToken`. Cada aplicación cliente, correspondiente a una integración específica, como Claude, ChatGPT o n8n, se registra de forma individual y queda asociada a un único espacio de trabajo. El token de acceso emitido para dicha aplicación hereda esta asociación de forma desnormalizada, lo que permite al servidor MCP identificar el workspace correspondiente a cada solicitud sin necesidad de consultas adicionales sobre la aplicación de origen.

## 2. Autorización en dos capas

Una vez autenticada la solicitud, el sistema aplica un proceso de autorización en dos capas, centralizado en el método `get_queryset()` de la clase `ScopedQueryToolset`, del cual heredan las herramientas y colecciones expuestas por el servidor MCP:

1. **Validación de scope OAuth:** el sistema verifica que el token de acceso cuente con el alcance (scope) requerido por la herramienta o colección solicitada, mediante `token.allow_scopes([required_scope])`. Esta capa determina qué dominio de datos puede consultar la aplicación cliente (por ejemplo, `assignments:read`, `clients:read`, `users:read`).
2. **Verificación de permiso de workspace:** cuando la herramienta lo requiere, el sistema evalúa si el usuario autenticado cuenta con el permiso correspondiente dentro de su espacio de trabajo, mediante `has_workspace_permission(...)`. Esta capa restringe qué puede ver el usuario específicamente dentro del workspace al que pertenece, independientemente de que su token ya haya superado la validación de scope.

Superadas ambas validaciones, la consulta se delega al queryset propio de la colección o herramienta, el cual aplica un filtrado adicional por workspace antes de ejecutarse contra la base de datos, reforzando el aislamiento de datos entre clientes.

## 3. Aislamiento de datos (multi-tenancy)

El aislamiento de datos entre empresas cliente se garantiza mediante el filtrado consistente por workspace en cada nivel del sistema: el token de acceso porta el identificador de su workspace de origen, cada herramienta y colección restringe sus resultados al workspace del token autenticado, y el modelo de datos desnormaliza esta relación para evitar accesos cruzados accidentales entre espacios de trabajo distintos (RNF-07).

## 4. Registro y trazabilidad

Toda solicitud atendida por el servidor MCP, exitosa o fallida, es registrada mediante el modelo `MCPLogs`, el cual almacena la herramienta invocada, los datos de entrada y salida, el resultado de la operación, los errores producidos y metadatos de la solicitud, incluyendo usuario, aplicación, dirección IP y tiempo de respuesta. Este mecanismo da soporte directo a RF-09 y constituye, adicionalmente, un componente de trazabilidad de seguridad ante eventuales incidentes o accesos indebidos.

## 5. Casos particulares y limitaciones identificadas

No todas las herramientas y colecciones del sistema implementan ambas capas de autorización de manera uniforme. Las colecciones `workspace` y `totalstats` únicamente declaran el scope OAuth requerido, sin contar con un permiso de workspace asociado (`required_permissions` vacío). Asimismo, las herramientas `ping` y `get_server_instructions` no realizan validación propia de scope ni de permiso, dado que corresponden a endpoints de metadata sin acceso a datos operativos del workspace, y dependen exclusivamente de la autenticación general provista por el middleware del servidor MCP. Estas particularidades se documentan de forma transparente como parte del diseño actual del sistema, y se identifican como un punto de mejora a considerar en futuras iteraciones del proyecto.
