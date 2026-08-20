# Descripción del proyecto

## Situación actual

Actualmente, para obtener información operativa de campo, los usuarios de la empresa cliente dependen de la descarga de archivos planos (formatos XLSX/CSV) que contienen los datos crudos del sistema. Estos archivos no constituyen un análisis en sí mismos, sino únicamente la materia prima sobre la cual debe trabajarse.

El procesamiento y análisis de dicha información recae normalmente en un tercero, un analista de la empresa cliente, quien debe manipular manualmente las hojas de cálculo para generar reportes, responder preguntas puntuales o identificar tendencias. Este proceso es variable en duración, pudiendo tomar desde medio día hasta un día completo dependiendo de la complejidad de la consulta y la disponibilidad del analista.

Esta dependencia genera varios problemas: los operadores de campo no pueden resolver dudas operativas de forma inmediata, la generación de análisis está condicionada a la disponibilidad de una persona específica, y el manejo manual de archivos planos es propenso a errores y consume tiempo valioso que podría dedicarse a la toma de decisiones.

## Situación deseable

El sistema propuesto elimina la dependencia de un intermediario humano para la obtención y el análisis básico de datos operativos. A través de un Agente de Inteligencia Artificial conectado al sistema mediante el Protocolo de Contexto de Modelo (MCP), el propio usuario operador puede formular preguntas en lenguaje natural y obtener respuestas o análisis generados a partir de los datos operativos necesarios, sin necesidad de descargar archivos planos ni depender de un analista intermedio.

De esta forma, el tiempo de respuesta se reduce de un proceso que hoy toma medio día o más, a una interacción prácticamente inmediata, ya que el Agente de IA cuenta con la capacidad de identificar, obtener y procesar los datos necesarios de forma autónoma, respetando en todo momento los controles de acceso y aislamiento de información propios de la arquitectura multi-tenant del sistema.
