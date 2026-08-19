# Reglas de Negocio

Las siguientes reglas de negocio establecen restricciones y políticas que el sistema debe respetar de forma constante, independientemente de la herramienta o funcionalidad que se esté ejecutando. Estas reglas se derivan directamente del modelo de seguridad y del carácter multi-tenant de la arquitectura propuesta.

## RN-01 Asociación única de aplicación a workspace

Cada aplicación cliente (agente de inteligencia artificial registrado como cliente MCP) pertenece a un único espacio de trabajo. Una misma aplicación no puede operar simultáneamente para más de un workspace.

## RN-02 Aislamiento absoluto de datos por workspace

Ninguna solicitud, independientemente de la herramienta invocada o del usuario que la origine, puede acceder a datos pertenecientes a un espacio de trabajo distinto al asociado con el token de acceso utilizado. Esta regla constituye la política de aislamiento fundamental del sistema.

## RN-03 Doble validación de autorización

El acceso a cualquier herramienta o colección que exponga datos operativos requiere superar dos validaciones independientes: la verificación del alcance (scope) autorizado por OAuth2, y la verificación del permiso específico del usuario dentro de su espacio de trabajo, cuando la herramienta lo requiera. Ninguna de las dos validaciones sustituye a la otra.

## RN-04 Registro obligatorio de todas las solicitudes

Toda solicitud atendida por el servidor MCP debe quedar registrada, sea esta exitosa o fallida, sin excepciones. El registro debe incluir la herramienta invocada, los datos de entrada y salida, el resultado de la operación y los metadatos asociados a la solicitud.

## RN-05 Excepción de permisos para metadatos generales

Las colecciones de metadatos generales (workspace, totalstats) y las herramientas de utilidad (ping, get_server_instructions) están exentas de la validación de permiso de workspace, ya que no exponen datos operativos específicos de una empresa cliente. Esta excepción es una decisión de diseño documentada explícitamente y no constituye una omisión.

## RN-06 Sistema de solo lectura

El sistema no contempla, bajo ninguna circunstancia, operaciones de creación, actualización o eliminación de datos operativos a través de las herramientas MCP. Toda interacción se limita exclusivamente a la consulta (lectura) de información.
