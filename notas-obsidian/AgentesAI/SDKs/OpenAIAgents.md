[[SDKs]]
[SDK de OpenAI](https://openai.github.io/openai-agents-python/)

Aquí tienes un **overview básico** del **SDK de OpenAI para agentes** (Agents SDK), sus componentes clave, casos de uso, ventajas y retos. Si quieres, puedo mostrarte ejemplos concretos de código.

---

## ¿Qué es el Agents SDK?

El Agents SDK es una librería (actualmente con uso principal en Python, y también en TypeScript/JavaScript) que permite construir “agentes” basados en modelos de lenguaje (LLMs) que no solo generan texto, sino que pueden **razonar**, **invocar herramientas / funciones**, **delegar tareas entre agentes** y **mantener estado** en flujos de conversación o tareas más complejas. ([OpenAI GitHub Pages](https://openai.github.io/openai-agents-python/?utm_source=chatgpt.com "OpenAI Agents SDK"))

Está inspirado en experimentos anteriores (como “Swarm”) y busca ofrecer un conjunto reducido de primitivas bien pensadas para crear agentes en producción con un coste de aprendizaje moderado. ([OpenAI](https://openai.com/index/new-tools-for-building-agents/?utm_source=chatgpt.com "New tools for building agents | OpenAI"))

---

## Componentes / primitivas clave

Aquí los elementos más importantes del SDK:

|Componente|Qué hace / para qué sirve|
|---|---|
|**Agent (agente)**|Representa un modelo con un conjunto de instrucciones (prompt/instrucciones), herramientas, reglas (guardrails) y posibilidad de delegar tareas. ([OpenAI GitHub Pages](https://openai.github.io/openai-agents-python/agents/?utm_source=chatgpt.com "Agents - OpenAI Agents SDK"))|
|**Tools / funciones (function tools)**|Puedes convertir funciones Python en “herramientas” que el agente puede llamar con parámetros estructurados, y el SDK se encarga de validación de entrada/salida. ([OpenAI GitHub Pages](https://openai.github.io/openai-agents-python/?utm_source=chatgpt.com "OpenAI Agents SDK"))|
|**Runner**|Encargado de ejecutar al agente: manejar el bucle de razonamiento, llamadas a herramientas, reenvíos al modelo, hasta que se determina que la tarea está “completada”. ([DEV Community](https://dev.to/composiodev/openai-agents-sdk-a-step-by-step-guide-to-building-real-world-mcp-agents-with-composio-4f92?utm_source=chatgpt.com "OpenAI Agents SDK: A Step-by-Step Guide to Building Real-World ..."))|
|**Handoffs / delegaciones**|Un agente puede delegar ciertas subtareas a otros agentes especializados. Esto permite arquitecturas de múltiples agentes colaborando. ([OpenAI GitHub Pages](https://openai.github.io/openai-agents-python/?utm_source=chatgpt.com "OpenAI Agents SDK"))|
|**Guardrails (reglas de protección)**|Validaciones o filtros que se ejecutan para asegurar que las entradas o salidas cumplen ciertos criterios o restricciones, prevenir errores o respuestas no deseadas. ([OpenAI GitHub Pages](https://openai.github.io/openai-agents-python/?utm_source=chatgpt.com "OpenAI Agents SDK"))|
|**Sessions / memoria de contexto**|Mecanismo para mantener el historial de la conversación o del agente a través de múltiples interacciones, de modo que el agente “recuerde” lo que pasó anteriormente. ([GitHub](https://github.com/openai/openai-agents-python?utm_source=chatgpt.com "openai/openai-agents-python: A lightweight, powerful ... - GitHub"))|
|**Tracing / observabilidad**|El SDK genera trazas automáticas de la ejecución del agente (qué herramientas invocó, con qué parámetros, en qué secuencia), lo que facilita depuración, monitoreo y evaluación. ([GitHub](https://github.com/openai/openai-agents-python?utm_source=chatgpt.com "openai/openai-agents-python: A lightweight, powerful ... - GitHub"))|
|**Durable Execution / integración con Temporal**|Para tareas de larga duración o recuperación frente a fallos, hay integración con **Temporal** para que los flujos del agente sean resistentes ante reinicios, interrupciones, timeouts, etc. ([temporal.io](https://temporal.io/blog/announcing-openai-agents-sdk-integration?utm_source=chatgpt.com "Production-ready agents with the OpenAI Agents SDK + Temporal"))|

---

## Flujo de operación / modelo mental

Una forma de verlo es:

1. Creas un agente con instrucciones, herramientas, etc.
    
2. Llamas al agente mediante el `Runner`, pasando una entrada (prompt, pregunta, tarea).
    
3. El agente internamente puede:
    
    - Generar una respuesta directamente si es “simple”,
        
    - O decidir llamar a una herramienta (o varias) para obtener datos externos o realizar acciones,
        
    - Luego reintegrar esos resultados al razonamiento del agente,
        
    - Repetir ese ciclo (“loop”) hasta que el agente decide que ha cumplido la tarea.
        
4. Si se definieron **handoffs**, en algún punto podría delegar a otro agente más especializado.
    
5. Durante todo esto, se genera trazabilidad para ver qué paso hizo qué cosa, y las **guardrails** pueden detener el agente si se detecta alguna violación o salida no deseada.
    
6. Si hay una sesión con memoria, las interacciones anteriores se tienen en cuenta en futuras invocaciones.
    

Este modelo permite construir agentes no triviales, con múltiples pasos, con razonamiento intermediario y uso de herramientas externas. ([Medium](https://mtugrull.medium.com/unpacking-openais-agents-sdk-a-technical-deep-dive-into-the-future-of-ai-agents-af32dd56e9d1?utm_source=chatgpt.com "Unpacking OpenAI's Agents SDK: A Technical Deep Dive into the ..."))

---

## Ventajas / beneficios

Algunas de las fortalezas que ofrece este enfoque:

- **Abstracción moderada pero no excesiva**: No es un framework con mil capas encantadas, sino con pocas primitivas claramente definidas. ([OpenAI GitHub Pages](https://openai.github.io/openai-agents-python/?utm_source=chatgpt.com "OpenAI Agents SDK"))
    
- **Flexibilidad / personalización**: Puedes adaptar casi todo: instrucciones dinámicas, reglas, estrategias de delegación, etc. ([GitHub](https://github.com/openai/openai-agents-python?utm_source=chatgpt.com "openai/openai-agents-python: A lightweight, powerful ... - GitHub"))
    
- **Observabilidad / trazas integradas**: Lo que ocurre “dentro” del agente puede ser monitoreado/perseguido. ([GitHub](https://github.com/openai/openai-agents-python?utm_source=chatgpt.com "openai/openai-agents-python: A lightweight, powerful ... - GitHub"))
    
- **Preparado para producción**: Con integraciones como Temporal para durabilidad, manejo de fallos, reinicios, etc. ([temporal.io](https://temporal.io/blog/announcing-openai-agents-sdk-integration?utm_source=chatgpt.com "Production-ready agents with the OpenAI Agents SDK + Temporal"))
    
- **Reutilización y modularidad**: Agentes especializados pueden colaborarse (mediante handoffs) en arquitecturas más limpias.
    
- **Menor esfuerzo de ingeniería**: No hay que construir desde cero toda la lógica de control de herramientas / orquestación.
    

---

## Limitaciones / retos / cosas a considerar

No es magia absoluta; hay aspectos que debes vigilar:

- **Costos de invocación del modelo y latencia**: Cada vez que el agente llama al modelo, hay consumo y latencia, y si el agente hace muchos pasos intermedios, se puede encarecer o ralentizar.
    
- **Correctitud / errores en las herramientas**: Si una herramienta retorna algo inesperado o erróneo, el agente puede “caer”. Las guardrails ayudan, pero no eliminan todos los riesgos.
    
- **Control de loops / bucles infinitos**: Si el agente no detecta bien cuándo “terminar”, puede seguir generando llamadas repetitivas sin fin.
    
- **Complejidad en arquitecturas multi-agente**: Coordinar muchos agentes con delegaciones puede complicar el diseño del sistema, especialmente con conflictos de dependencias o señales cruzadas.
    
- **Dependencia de modelos tipo Chat Completions**: El SDK está muy acoplado a modelos que aceptan ese tipo de interfaz; otros modelos que no sigan ese estilo podrían necesitar adaptadores. ([OpenAI](https://openai.com/index/new-tools-for-building-agents/?utm_source=chatgpt.com "New tools for building agents | OpenAI"))
    
- **Seguridad, validaciones y “inyección de prompt”**: Cuando los agentes usan herramientas o interactúan con sistemas externos, necesitas asegurarte de que no se produzcan comportamientos inesperados o maliciosos.
    
- **Limitaciones de memoria / contexto**: Si el historial crece mucho, mantener contexto completo puede ser costoso o inviable.
    
- **Transición entre tareas largas / estado persistente**: Si el agente debe realizar tareas que toman mucho tiempo o cruzar reinicios, hace falta utilizar soluciones como la integración con Temporal. ([temporal.io](https://temporal.io/blog/announcing-openai-agents-sdk-integration?utm_source=chatgpt.com "Production-ready agents with the OpenAI Agents SDK + Temporal"))
    

---

## Casos de uso típicos

Este tipo de SDK es útil para muchas aplicaciones “agentivas”:

- Automatización de atención al cliente / soporte, donde el agente puede consultar base de datos, historiales, APIs externas. ([OpenAI](https://openai.com/index/new-tools-for-building-agents/?utm_source=chatgpt.com "New tools for building agents | OpenAI"))
    
- Flujos de investigación o asistencia técnica que requieren múltiples pasos (buscar web, resumir, combinar resultados). ([OpenAI](https://openai.com/index/new-tools-for-building-agents/?utm_source=chatgpt.com "New tools for building agents | OpenAI"))
    
- Agentes internos de empresa para procesar documentos, responder consultas específicas del dominio.
    
- Orquestación de decisiones o pipelines inteligentes donde el agente decide qué herramienta llamar y cuándo.
    
- Tareas con delegaciones: por ejemplo, un agente “gestor” que decide si delegar a un agente “especialista” según la naturaleza de la consulta.
    
- Procesos largos o distribuibles, mediante integración con infraestructuras de orquestación (por ejemplo, Temporal) para tolerancia a fallos y reinicios. ([temporal.io](https://temporal.io/blog/announcing-openai-agents-sdk-integration?utm_source=chatgpt.com "Production-ready agents with the OpenAI Agents SDK + Temporal"))
    

---

