# Alcance

El presente proyecto delimita su alcance a la implementación de un sistema de **consulta de datos operativos en modalidad de solo lectura (read-only)**, accesible mediante herramientas expuestas a través del Protocolo de Contexto de Modelo (MCP).

**Dentro del alcance:**

* Exposición de herramientas (tools) MCP que permiten al Agente de IA consultar datos operativos de campo pertenecientes al workspace autorizado del usuario.
* Autenticación y autorización de las solicitudes mediante OAuth2, garantizando que cada consulta se realice dentro de los límites de acceso correspondientes al usuario y a su empresa cliente (workspace).
* Aislamiento multi-tenant de la información, asegurando que ningún usuario pueda acceder a datos de un workspace distinto al suyo.
* Registro y auditoría de las interacciones realizadas por el Agente de IA a través del sistema (MCPLogs).
* Entrega de los datos operativos solicitados en un formato que el Agente de IA externo pueda interpretar para generar análisis, respuestas o resúmenes en lenguaje natural.

**Fuera del alcance:**

* Operaciones de creación, actualización o eliminación (Create, Update, Delete) de datos operativos a través del sistema MCP. El sistema desarrollado en este proyecto se limita exclusivamente a operaciones de lectura (Read).
* El desarrollo, entrenamiento o control del Agente de IA utilizado por el usuario. El agente es un componente externo elegido libremente por el usuario; el sistema únicamente expone y protege el contrato de herramientas que dicho agente puede consumir.
* La validación de la calidad, precisión o interpretación del análisis generado por el Agente de IA a partir de los datos entregados.

El desarrollo, prueba e implementación funcional del sistema descrito debe estar completado a más tardar el 31 de octubre, conforme al ciclo de vida establecido en el cronograma de actividades adjunto a este documento.
