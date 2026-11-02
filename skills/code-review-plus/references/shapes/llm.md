# Shape — LLM / agent surface

Treat the model as an untrusted component. Prompts, retrieved documents, and tool output can carry attacker instructions.

## Ask

- Can untrusted content make the model call a tool or reach data that the caller cannot reach through the normal API?
- Does server code authorize each tool call for the current user and tenant? A system prompt is not a control.
- Do model output or tool arguments reach an HTML, SQL, shell, file, or network sink without the checks applied to user input?
- Are secrets or other users' data sent to the model or to model-facing logs?

User content inside a prompt is not a finding alone. Keep it when it leads to an action or a data gain above.
