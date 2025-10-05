[[SDKs]]
[Docs de Vertex](https://cloud.google.com/vertex-ai/docs)

---

## ¿Qué es Vertex AI Agent SDK / Agent Builder / Agent Engine?

Vertex AI (la plataforma de IA de Google Cloud) ha introducido un conjunto de herramientas centradas en construir, desplegar y operar agentes inteligentes generativos. Estas herramientas abarcan tanto la parte de desarrollo (SDK / Agent Development Kit) como la infraestructura gestionada para producción (Agent Engine). ([Google Cloud](https://cloud.google.com/vertex-ai/generative-ai/docs/agent-engine/overview?utm_source=chatgpt.com "Vertex AI Agent Engine overview - Google Cloud"))

Algunas definiciones de componentes importantes:

- **Vertex AI Agent Engine**: es el entorno gestionado que permite desplegar, escalar y operar agentes en producción. Proporciona runtime, observabilidad, manejo de sesiones, memoria persistente, trazas, etc. ([Google Cloud](https://cloud.google.com/vertex-ai/generative-ai/docs/agent-engine/overview?utm_source=chatgpt.com "Vertex AI Agent Engine overview - Google Cloud"))
    
- **Agent Builder / Agent Development Kit (ADK)**: es el kit de desarrollo (open source) que facilita crear agentes (incluyendo multi-agentes) con lógica, herramientas, integración de modelos, debugging local y despliegue a Agent Engine u otros entornos. ([Google Cloud](https://cloud.google.com/vertex-ai/generative-ai/docs/agent-builder/overview?utm_source=chatgpt.com "Vertex AI Agent Builder overview - Google Cloud"))
    
- **Agent Garden**: una colección de agentes y herramientas preconstruidos que puedes usar como punto de partida o inspiración (plantillas). ([Google Cloud](https://cloud.google.com/vertex-ai/generative-ai/docs/agent-builder/overview?utm_source=chatgpt.com "Vertex AI Agent Builder overview - Google Cloud"))
    
- **Herramientas (Tools / integraciones)**: mecanismos que el agente puede invocar para hacer búsquedas, ejecutar código, consultar bases de datos, APIs externas, etc. Ejemplo: `VertexAiSearchTool`. ([google.github.io](https://google.github.io/adk-docs/grounding/vertex_ai_search_grounding/?utm_source=chatgpt.com "Understanding Vertex AI Search Grounding - Agent Development Kit"))
    
- **Sesiones / memoria**: mecanismos gestionados para que los agentes “recuerden” el estado entre interacciones, mantener contexto, almacenar interacciones pasadas. ([Google Cloud](https://cloud.google.com/vertex-ai/generative-ai/docs/agent-engine/overview?utm_source=chatgpt.com "Vertex AI Agent Engine overview - Google Cloud"))
    
- **Evaluación / métricas / trazabilidad**: capacidades para evaluar la calidad del agente (respuestas finales y pasos intermedios), registrar trazas (logs, eventos), integrarse con sistemas de monitoreo de Google Cloud (Cloud Logging, Cloud Trace) ([Google Cloud](https://cloud.google.com/vertex-ai/generative-ai/docs/agent-engine/overview?utm_source=chatgpt.com "Vertex AI Agent Engine overview - Google Cloud"))
    
- **Despliegue / runtime gestionado**: el backend gestiona el contenedor del agente, escalado automático, seguridad, configuración de entorno, etc. ([Google Cloud](https://cloud.google.com/vertex-ai/generative-ai/docs/agent-engine/overview?utm_source=chatgpt.com "Vertex AI Agent Engine overview - Google Cloud"))
    

---

## Flujo de uso / modelo mental

Una visión simplificada de cómo trabajarías con este SDK/plataforma:

1. **Preparar el entorno en Google Cloud**
    
    - Crear un proyecto, habilitar APIs necesarias (Vertex AI, etc.) ([Google Cloud](https://cloud.google.com/vertex-ai/generative-ai/docs/agent-development-kit/quickstart?utm_source=chatgpt.com "Quickstart: Build an agent with the Agent Development Kit"))
        
    - Configurar autenticación (service accounts / credenciales) ([Google Developer forums](https://discuss.google.dev/t/how-to-connect-adk-agents-to-vertex-ai-api-key-setup-issue/186935?utm_source=chatgpt.com "How to Connect ADK agents to Vertex AI (API key setup issue)"))
        
2. **Desarrollar tu agente localmente con ADK**
    
    - Definir el agente (modelo base, instrucciones, herramientas, etc.) usando las clases del SDK. ([Google Cloud](https://cloud.google.com/vertex-ai/generative-ai/docs/agent-builder/overview?utm_source=chatgpt.com "Vertex AI Agent Builder overview - Google Cloud"))
        
    - Probar localmente (modo “dev”) con sesiones en memoria, simular llamadas a herramientas, depurar trazas ([google.github.io](https://google.github.io/adk-docs/deploy/agent-engine/?utm_source=chatgpt.com "Deploy to Vertex AI Agent Engine - Google"))
        
3. **Preparar para desplegar en producción**
    
    - Envolver tu agente en objetos específicos del SDK para que sean compatibles con Agent Engine (por ejemplo, `AdkApp`) ([google.github.io](https://google.github.io/adk-docs/deploy/agent-engine/?utm_source=chatgpt.com "Deploy to Vertex AI Agent Engine - Google"))
        
    - Empaquetar tu código, dependencias, contenedores, etc. ([google.github.io](https://google.github.io/adk-docs/deploy/agent-engine/?utm_source=chatgpt.com "Deploy to Vertex AI Agent Engine - Google"))
        
4. **Desplegar en Agent Engine / entorno gestionado**
    
    - Enviar el agente al runtime gestionado (Agent Engine) donde se ejecutará bajo demanda. ([Google Cloud](https://cloud.google.com/vertex-ai/generative-ai/docs/agent-engine/overview?utm_source=chatgpt.com "Vertex AI Agent Engine overview - Google Cloud"))
        
    - El runtime se encarga del escalado, seguridad, manejo de recursos, logging / trazabilidad. ([Google Cloud](https://cloud.google.com/vertex-ai/generative-ai/docs/agent-engine/overview?utm_source=chatgpt.com "Vertex AI Agent Engine overview - Google Cloud"))
        
5. **Interactuar y operar el agente**
    
    - Envío de consultas (requests) al agente desplegado (por API).
        
    - Uso de sesiones persistentes: cada usuario/interacción puede mantener historial / contexto. ([Google Cloud](https://cloud.google.com/vertex-ai/generative-ai/docs/agent-engine/overview?utm_source=chatgpt.com "Vertex AI Agent Engine overview - Google Cloud"))
        
    - Monitoreo, logs, evaluación continua del desempeño del agente.
        

---

## Ventajas / fortalezas

Estas son algunas de las ventajas que aporta este enfoque de agente en Vertex AI:

- **Infraestructura gestionada**: no tienes que construir toda la lógica de despliegue, escalado, contenedores, logging desde cero. El Agent Engine ofrece runtime administrado. ([Google Cloud](https://cloud.google.com/vertex-ai/generative-ai/docs/agent-engine/overview?utm_source=chatgpt.com "Vertex AI Agent Engine overview - Google Cloud"))
    
- **Interoperabilidad con frameworks existentes**: puedes construir agentes con ADK o con frameworks populares como LangChain, LangGraph, AG2, etc., y desplegarlos sobre Agent Engine. ([Google Cloud](https://cloud.google.com/vertex-ai/generative-ai/docs/agent-engine/overview?utm_source=chatgpt.com "Vertex AI Agent Engine overview - Google Cloud"))
    
- **Herramientas integradas / grounding**: facilidades para que el agente invoque herramientas, haga búsquedas, interactúe con datos, etc., sin que tengas que reinventar todo. ([Google Cloud](https://cloud.google.com/vertex-ai/generative-ai/docs/agent-builder/overview?utm_source=chatgpt.com "Vertex AI Agent Builder overview - Google Cloud"))
    
- **Persistencia de estado / sesiones / memoria**: el agente puede “recordar” interacciones pasadas de manera gestionada. ([Google Cloud](https://cloud.google.com/vertex-ai/generative-ai/docs/agent-engine/overview?utm_source=chatgpt.com "Vertex AI Agent Engine overview - Google Cloud"))
    
- **Trazabilidad y evaluación integrada**: puedes ver cada paso del agente, no sólo la respuesta final, y evaluar calidad de respuestas intermedias y finales. ([Google Cloud](https://cloud.google.com/vertex-ai/generative-ai/docs/agent-builder/overview?utm_source=chatgpt.com "Vertex AI Agent Builder overview - Google Cloud"))
    
- **Seguridad y cumplimiento**: soporte para redes privadas (VPC Service Controls), encriptación, control de accesos mediante IAM, etc. ([Google Cloud](https://cloud.google.com/vertex-ai/generative-ai/docs/agent-engine/overview?utm_source=chatgpt.com "Vertex AI Agent Engine overview - Google Cloud"))
    
- **Escalabilidad**: el agente puede ser escalado según demanda dentro de la infraestructura de Google Cloud. ([Google Cloud](https://cloud.google.com/vertex-ai/generative-ai/docs/agent-engine/overview?utm_source=chatgpt.com "Vertex AI Agent Engine overview - Google Cloud"))
    
- **Flexibilidad de modelo**: puedes usar modelos de Google (Gemini u otros) pero también integrar otros modelos o endpoints personalizados. ([google.github.io](https://google.github.io/adk-docs/agents/models/?utm_source=chatgpt.com "Models & Authentication - Agent Development Kit - Google"))
    

---

## Limitaciones, retos o puntos a vigilar

No todo es perfecto: hay aspectos que conviene tener en cuenta o que aún están en desarrollo:

- **Estado de preview / evolución constante**: algunas funciones están en vista previa (memory bank, sesiones, ejemplo store, code execution) y pueden cambiar. ([Google Cloud](https://cloud.google.com/vertex-ai/generative-ai/docs/agent-engine/overview?utm_source=chatgpt.com "Vertex AI Agent Engine overview - Google Cloud"))
    
- **Complejidad adicional para flujos simples**: para casos muy simples, puede parecer un sobrecosto tener toda la infraestructura de agentes completa.
    
- **Latencia / costos adicionales**: desplegar agentes, invocar herramientas, mantener memoria persistente, trazabilidad — todo eso añade overhead en latencia y coste computacional.
    
- **Restricciones regionales / disponibilidad**: algunas características pueden no estar disponibles en todas las regiones. ([Google Cloud](https://cloud.google.com/vertex-ai/generative-ai/docs/agent-engine/overview?utm_source=chatgpt.com "Vertex AI Agent Engine overview - Google Cloud"))
    
- **Aprendizaje de nuevas abstracciones**: trabajar con ADK, sessions, memoria, wrapping del agente para Agent Engine, etc., supone algo de curva de aprendizaje.
    
- **Dependencia de Google Cloud**: aunque puedes correr agentes localmente o en contenedores propios, muchas de las ventajas (runtime gestionado, observabilidad) dependen del ecosistema de GCP.
    
- **Control granular vs “caja negra”**: parte de la infraestructura está abstraída; si necesitas ajustes muy finos del runtime puede no ser tan trivial.
    

---
