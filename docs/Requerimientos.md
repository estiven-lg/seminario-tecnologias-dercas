# Requerimientos

## Requerimientos Funcionales

Los requerimientos funcionales especifican las operaciones que debe proporcionar el sistema para permitir la interacción con las herramientas MCP y la ejecución de las capacidades analíticas definidas. Estos requerimientos contemplan aspectos como la autenticación, interpretación de consultas en lenguaje natural, selección y ejecución de herramientas, generación de respuestas y manejo de errores.

**Tabla 1: Requerimientos Funcionales**

| ID    | Nombre                                     | Descripción                                                                                                                                                                               |
| ----- | ------------------------------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| RF-01 | Autenticación de usuarios                  | El sistema debe autenticar al usuario mediante el servidor OAuth antes de permitir la invocación de cualquier herramienta MCP protegida.                                                  |
| RF-02 | Autorización por espacio de trabajo        | El sistema debe verificar que el usuario autenticado tenga autorización para acceder al espacio de trabajo (empresa cliente) correspondiente antes de ejecutar cualquier herramienta MCP. |
| RF-03 | Interpretación y selección de herramientas | El sistema debe interpretar consultas formuladas en lenguaje natural, determinar la intención del usuario y seleccionar la o las herramientas MCP necesarias para resolverla.             |
| RF-04 | Ejecución de herramientas MCP              | El sistema debe ejecutar las herramientas MCP seleccionadas sobre los modelos Django correspondientes, restringiendo el acceso a los datos del espacio de trabajo autorizado del usuario. |
| RF-05 | Ejecución de capacidades analíticas        | El sistema debe ejecutar capacidades analíticas sobre los datos operativos de campo mediante herramientas MCP especializadas, cuando la consulta del usuario lo requiera.                 |
| RF-06 | Generación de respuestas estructuradas     | El sistema debe utilizar los resultados obtenidos mediante las herramientas MCP para generar una respuesta estructurada relacionada con la consulta del usuario.                          |
| RF-07 | Manejo de consultas ambiguas o incompletas | El sistema debe identificar consultas ambiguas, incompletas o no interpretables, y solicitar información adicional al usuario o informar que la consulta no puede procesarse.             |
| RF-08 | Manejo de errores de ejecución             | El sistema debe proporcionar mensajes de error estructurados y comprensibles ante parámetros inválidos, ausencia de datos o fallos de conexión durante la ejecución de una herramienta.   |
| RF-09 | Registro de operaciones                    | El sistema debe registrar las invocaciones de herramientas MCP, incluyendo información de entrada, resultados obtenidos y errores producidos.                                             |
| RF-10 | Exposición de herramientas MCP             | El sistema debe exponer las herramientas registradas mediante el servidor MCP, permitiendo su invocación desde cualquier cliente MCP compatible.                                          |

## Requerimientos No Funcionales

Los requerimientos no funcionales definen las condiciones de calidad, seguridad, interoperabilidad, mantenibilidad y restricciones técnicas que debe cumplir la solución propuesta.

**Tabla 2: Requerimientos No Funcionales**

| ID     | Nombre                            | Descripción                                                                                                                                                                                                                                     |
| ------ | --------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| RNF-01 | Usabilidad                        | El sistema debe proporcionar una interacción que permita a los usuarios realizar consultas de datos operativos mediante lenguaje natural sin requerir conocimiento de la estructura interna de las herramientas MCP.                            |
| RNF-02 | Interoperabilidad                 | El servidor MCP debe implementar el protocolo de comunicación establecido para permitir la interacción con clientes MCP compatibles sin requerir modificaciones específicas en el cliente.                                                      |
| RNF-03 | Seguridad                         | El sistema debe restringir el acceso a las herramientas MCP mediante mecanismos de autenticación y autorización, y proteger las comunicaciones entre sus componentes mediante protocolos de cifrado.                                            |
| RNF-04 | Estandarización de respuestas     | Las herramientas MCP deben proporcionar respuestas utilizando una estructura de datos estandarizada que permita su procesamiento uniforme por los clientes compatibles.                                                                         |
| RNF-05 | Mantenibilidad                    | Las herramientas MCP deben mantener una estructura modular que permita incorporar, modificar o retirar capacidades analíticas sin afectar las demás herramientas implementadas.                                                                 |
| RNF-06 | Compatibilidad de infraestructura | El sistema debe operar dentro de los recursos de infraestructura definidos para el entorno piloto, incluyendo la instancia AWS EC2 seleccionada.                                                                                                |
| RNF-07 | Aislamiento de datos              | El sistema debe garantizar que las consultas e invocaciones de herramientas MCP solo permitan acceder a los datos pertenecientes al espacio de trabajo autorizado del usuario, impidiendo el acceso a información de otros espacios de trabajo. |
