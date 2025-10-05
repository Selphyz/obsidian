[[SDKs]]
[Link a DOCs](https://www.langchain.com/langgraph)
### LangChain

- LangChain es un framework (biblioteca) para construir aplicaciones que usan modelos de lenguaje (LLMs) como componentes centrales. ([Wikipedia](https://en.wikipedia.org/wiki/LangChain?utm_source=chatgpt.com "LangChain"))
    
- Incluye utilidades para “cadenas” (chains) de llamadas, integración con “herramientas” externas (APIs, funciones, búsquedas, bases de datos), manejo de contexto, memory, etc. ([Simplilearn.com](https://www.simplilearn.com/langchain-vs-langgraph-article?utm_source=chatgpt.com "LangChain vs LangGraph: Key Differences Explained"))
    
- En cuanto a agentes, LangChain tiene una capa para construir agentes que toman decisiones, llaman herramientas, razonan, etc. Pero esa capa de agentes “tradicional” (AgentExecutor, etc.) se considera algo más limitada frente al nuevo paradigma de LangGraph. ([LangChain](https://python.langchain.com/api_reference/core/agents.html?utm_source=chatgpt.com "agents — LangChain documentation"))
    

### LangGraph

- LangGraph es una librería de orquestación de agentes “stateful” basada en grafos (o flujos explícitos) diseñada para construir agentes más complejos, con persistencia, manejo de estado, ramificaciones, reinicios y ejecución duradera. ([LangChain](https://langchain-ai.github.io/langgraph/?utm_source=chatgpt.com "LangGraph - GitHub Pages"))
    
- Fue creada por el equipo de LangChain (o al menos dentro de su ecosistema) como una evolución para construir agentes más robustos y con arquitecturas más controladas. ([LangChain](https://www.langchain.com/langgraph?utm_source=chatgpt.com "LangGraph - LangChain"))
    
- LangGraph permite definir flujos de tareas (nodos) y el paso de datos entre ellos, manejar interrupciones (por ejemplo “human-in-the-loop”), persistencia de memoria a largo plazo, ejecución duradera (checkpointing, reintentos) y más control sobre la orquestación del agente. ([LangChain Blog](https://blog.langchain.com/building-langgraph/?utm_source=chatgpt.com "Building LangGraph: Designing an Agent Runtime from first principles"))
    
- Tiene integración con herramientas de observabilidad como LangSmith, y una plataforma (LangGraph Platform / Server) para desplegar, escalar y monitorear agentes. ([LangChain](https://www.langchain.com/langgraph?utm_source=chatgpt.com "LangGraph - LangChain"))
    

---

## Filosofía / mentalidad / enfoque

Aquí algunas diferencias conceptuales clave:

|Aspecto|LangChain|LangGraph|
|---|---|---|
|Nivel de abstracción|Más “flexible, componible, manos sobre el código” (chains, herramientas)|Más de orquestación, flujos explícitos, control de estado y lógica de flujo|
|Enfoque de agentes|Agentes como una capa dentro del framework; tradicionalmente más “secuencial” o “paso a paso”|Agentes como grafos de tareas, con ramificación/flujo de control, persistencia, reentradas|
|Manejo de estado / memoria|Tiene mecanismos de memoria, pero típicamente más “momentáneo” / de contexto|Diseñado para persistencia, memoria a largo plazo, ejecución duradera|
|Robustez / resiliencia|Adecuado para flujos más simples o pipelines de transformación|Mejor para agentes que deben sobrevivir errores, reinicios, operaciones de larga duración|
|Flexibilidad / adaptabilidad|Muy vernáculo: puedes componer casi todo, integraciones abundantes|Similar flexibilidad, pero organizando la ejecución en grafos lo que da más control estructural|
|Curva de aprendizaje|Menos empinado para empezar, más “plug and play”|Requiere pensar en nodos, flujo de datos, control de estado, checkpointing, etc.|
|Observabilidad / trazas|Se pueden instrumentar los agentes, pero puede requerir trabajo extra o integraciones|Integrado con trazas, monitoreo, visualización del grafo de ejecución, estado de nodos, etc.|
|Dependencia / relación entre ambos|LangChain sigue siendo la base para muchas utilidades, herramientas, integraciones|LangGraph está construido sobre (o al lado) de LangChain y aprovecha muchas de sus integraciones. ([LangChain](https://python.langchain.com/api_reference/core/agents.html?utm_source=chatgpt.com "agents — LangChain documentation"))|

---

## Ventajas y desventajas comparadas

Aquí algunas ventajas, retos o limitaciones que cada uno tiene frente al otro, desde lo que se ha observado en la comunidad.

### Lo que LangChain hace bien

**Ventajas**

- Rapidez de prototipado: puedes encadenar modelos, herramientas y transformaciones de forma relativamente directa.
    
- Ecosistema amplio: muchas integraciones con APIs, bases de datos, librerías de embeddings, recuperación de texto, etc.
    
- Sencillez para flujos lineales o con ramificaciones simples.
    
- Comunidad establecida y abundante documentación, ejemplos, tutoriales.
    

**Desventajas / límites frente a lo que quiere resolver LangGraph**

- Manejo de agentes complejos con persistencia o reinicios a veces se vuelve “forzado”.
    
- Si el flujo de decisión tiene muchas ramas, loops, retroalimentaciones, puede complicarse mantenerlo claro.
    
- En escenarios donde el agente debe “pausar y reanudar” después de fallos, LangChain tradicional puede no proporcionar las herramientas adecuadas “de fábrica”.
    
- Menos control estructural sobre el flujo (por ejemplo, no es tan natural tener bucles o backtracking explícito).
    

### Lo que LangGraph hace bien (y los retos que trae)

**Ventajas**

- Orquestación explícita: el agente se define como un grafo de nodos, con relaciones de datos, dependencias, flujos de control claros.
    
- Estado persistente / memoria duradera: puedes tener memoria que sobreviva entre invocaciones del agente.
    
- Resiliencia / tolerancia a fallos: con checkpointing, reintentos automáticos, resumir ejecución después de interrupciones.
    
- Visualización y trazabilidad: ver qué nodos se ejecutaron, en qué orden, con qué datos, etc.
    
- Modularidad: flujos más complejos, subgrafos, delegaciones entre partes del grafo.
    
- Integración con infraestructuras de producción: plataformas de despliegue dedicadas, monitoreo, servidor de ejecución.
    
- Human-in-the-loop: más fácil interrumpir, inspeccionar el estado, modificar durante ejecución.
    
- Construcción de agentes “serios” (no solo “scripts LLM con herramientas”) con lógica de control más sofisticada.
    

**Desventajas / retos**

- Curva de aprendizaje más pronunciada: hay que pensar en grafos, nodos, flujos de control, checkpoints.
    
- Sobrecarga arquitectónica: para flujos simples puede resultar “demasiado” o agregar complejidad innecesaria.
    
- Gestión del entorno: tienes que encargarte del servidor, del estado, del almacenamiento, del despliegue si no usas la plataforma gestionada.
    
- Potencial costo en rendimiento o latencia si no se diseña bien el grafo o la orquestación.
    
- Puede ser excesivo cuando tu aplicación es más directa o lineal.
    

---

## Cuándo usar uno u otro (o combinarlos)

Aquí unas ideas de cuándo podría tener sentido elegir LangChain, LangGraph o una combinación:

- Si estás empezando, experimentando o tu aplicación es relativamente simple (una cadena de llamadas a modelo + herramientas), LangChain probablemente es suficiente y más ágil.
    
- Si tu agente debe operar en escenarios más “serios”: que puedan reiniciarse tras fallos, mantener memoria entre sesiones, tener ramificaciones complejas, o tener lógica de control elaborada — ahí LangGraph aporta mucho valor.
    
- Si ya estás usando LangChain para muchas integraciones, y tu aplicación empieza a crecer en complejidad de agente, puede hacer sentido migrar esa capa de agente hacia LangGraph mientras sigues usando las integraciones de LangChain (bases de datos, embeddings, proveedores de modelos, etc.).
    
- En producción, si necesitas escalado, monitoreo, tolerancia a fallos, estado duradero, LangGraph (y posiblemente su plataforma) se alinea mejor.
    
- En aplicaciones que realmente requieren “procesos autónomos largos” (por ejemplo, agentes que corren durante horas/días, o que tienen tareas cron, estados intermedios, delegaciones, etc.), LangGraph tiene una ventaja estructural.
    

---
