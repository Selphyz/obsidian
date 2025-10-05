[[SDKs]]

## Claude SDK

Es una colección de herramientas que ayuda a los desarrolladores a construir agentes potentes sobre Claude. Originalmente se llamaba "Claude Code SDK" pero fue renombrado para reflejar que puede usarse para crear agentes que van mucho más allá del código.

## Capacidades principales

El SDK te proporciona primitivas para construir agentes que operan en un bucle típico: **recopilar contexto → tomar acción → verificar trabajo → repetir**.

**Características clave:**

- **Gestión automática de contexto**: Compactación y manejo de contexto para que tu agente no se quede sin espacio
- **Herramientas integradas**: Operaciones de archivos, ejecución de código, búsqueda web, y extensibilidad con MCP
- **Subagentes**: Posibilidad de crear múltiples subagentes en paralelo, cada uno con su propio contexto aislado
- **Permisos avanzados**: Control granular sobre las capacidades del agente
- **Optimización para Claude**: Incluye prompt caching automático

## Tipos de agentes que puedes construir

El SDK permite crear diversos tipos de agentes como agentes financieros, asistentes personales, agentes de atención al cliente, agentes de investigación profunda y mucho más.

## Instalación básica

**Para Python** (requiere Python 3.10+):

```bash
pip install claude-agent-sdk
```

## Uso básico

```python
from claude_agent_sdk import query

async def main():
    async for message in query(prompt="¿Cuál es 2 + 2?"):
        print(message)
```

## Autenticación

Necesitas obtener una clave API de Claude desde la Consola de Claude y establecer la variable de entorno ANTHROPIC_API_KEY.

## Recursos

- **Documentación oficial**: https://docs.claude.com/en/api/agent-sdk/overview
- **Repositorio en GitHub**: https://github.com/anthropics/claude-agent-sdk-python
- Compatible con Claude Sonnet 4.5, el modelo más reciente y poderoso
