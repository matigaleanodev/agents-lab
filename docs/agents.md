# Agentes

Los archivos fuente están en `.codex/agents/`. No requieren un registro adicional en `config.toml` en clientes con soporte para agentes TOML independientes. Cada archivo define `name`, `description` y `developer_instructions`, según el [esquema oficial](https://learn.chatgpt.com/docs/agent-configuration/subagents).

| Rol | Resultado esperado | Edición |
| --- | --- | --- |
| `architect` | Recomendación con restricciones, alternativas, riesgos y plan | Solo si se pide explícitamente |
| `implementer` | Cambio delimitado y verificación relevante | Dentro de la tarea autorizada |
| `code-reviewer` | Hallazgos por gravedad, archivo, condición e impacto | Solo con autorización explícita |
| `security-reviewer` | Riesgos de seguridad con evidencia, impacto y corrección proporcionada | Sin ediciones |
| `test-engineer` | Estrategia y evaluación de pruebas priorizadas por riesgo; tests si se autorizan | Solo pruebas dentro del alcance autorizado |

No se fuerza modelo o esfuerzo. No hay ejecución automática ni cadenas de agentes. Para una tarea pequeña, el agente principal puede resolverla directamente.

`code-reviewer` conserva la revisión general. Reservá `security-reviewer` para auditorías o cambios en autenticación, autorización, IAM y configuración sensible; no ejecutes ambos por defecto. Revisa aplicaciones, AWS y CI según la evidencia, sin pruebas ofensivas sobre sistemas reales ni acceso innecesario a secretos.

`implementer` sigue escribiendo los tests normales de una funcionalidad. Usá `test-engineer` para estrategia, regresiones complejas, cobertura crítica, tests inestables o contratos relevantes. Reutiliza el framework existente y puede aplicar `api-contract-testing` si está disponible; no requiere instalarla ni modifica código productivo para hacer pasar tests.

Los roles no requieren dependencias nuevas. Su disponibilidad depende del soporte y la confianza del cliente; las skills se usan solo cuando correspondan.

```text
Delegá en architect el análisis de cómo dividir estos handlers, sin editar archivos.
Delegá en implementer el cambio aprobado en GET /items, preservando el contrato.
Delegá en code-reviewer la revisión del diff contra main; priorizá regresiones.
Delegá en security-reviewer la revisión de autorización de estos endpoints, sin editar ni consultar secretos.
Delegá en test-engineer el análisis de esta suite inestable y una propuesta de casos, sin editar.
```

Estos pedidos delegan trabajo, no crean un chat independiente del usuario. Los permisos son heredados: «no editar» es una instrucción del rol, no una barrera técnica de solo lectura. Elegí el sandbox del padre acorde al trabajo.

## Agregar o ajustar un agente

Creá un TOML por responsabilidad con nombre único y los tres campos requeridos. Hacé coincidir nombre de archivo y `name`. Escribí instrucciones breves y un resultado observable; no copies todas las preferencias globales.

Comprobá sintaxis TOML y descubrimiento con el cliente instalado. Validá comportamiento en una tarea acotada cuando se autorice delegación; verificá resultado y ausencia de efectos fuera de alcance.

Si el cliente no reconoce estos archivos, conservá el rol como referencia e incluí sus instrucciones manualmente en la tarea principal. No afirmes que un rol referenciado manualmente fue cargado como agente. No actualices el cliente ni agregues configuraciones antiguas por suposición.
