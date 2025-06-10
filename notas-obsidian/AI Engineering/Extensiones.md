
---
## Trucos Copilot

- **Especificar contexto**: Usa el símbolo **@** (y también **#** en Copilot) para proporcionar contexto específico a la IA.
- **Aprovechar la IA para _brainstorming_**: Utiliza las herramientas de IA para generar ideas y explorar diferentes enfoques.
- **Uso del _inline chat_**:
    - Emplea comandos como `[/doc`, `/edit`, `/explain`, `/fix`, `/generate`, `/tests]` para tareas rápidas y contextuales.
    - Selecciona texto antes de usar el _inline chat_ para dar a la IA un contexto más preciso.
- **Buscador de herramientas en Copilot**: Utiliza el buscador para encontrar _tools_, extensiones y **MCPs** (Microsoft Copilot Prompts) específicos.
- **Creación de _prompts_**: Guarda tus _prompts_ personalizados en la ruta `.github/prompts/**.md` para reutilizarlos y organizarlos.

### Configuraciones útiles de Copilot (a menudo desactivadas por defecto):

- **Comentarios previos y autocompletado por comentario**: Permite que Copilot sugiera código basado en los comentarios que escribes.
- `github.copilot.chat.codeGeneration.instructions`: Configura instrucciones específicas para la generación de código por parte de Copilot.
- `github.copilot.chat.agent.thinkingTool`: Habilita un modo de respuesta más lento pero más "reflexivo" por parte de la IA, ideal para problemas complejos.
- `github.copilot.nextEditSuggestions.enabled`: Activa el encadenamiento de sugerencias de edición en el editor, lo que permite un flujo de trabajo más continuo.

---