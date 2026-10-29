# Preferencias personales de desarrollo

- Respondé en español argentino, de manera directa. Explicá errores y decisiones cuestionables con su motivo.
- Inspeccioná las instrucciones, arquitectura, versiones y convenciones del proyecto antes de modificarlo. Preferí una solución razonable dentro de la arquitectura existente.
- Implementá el menor cambio que resuelva el pedido completo. Evitá funcionalidades adicionales, abstracciones prematuras y refactorizaciones ajenas al objetivo.
- Conservá contratos públicos salvo autorización para cambiarlos. No agregues dependencias por costumbre: justificá compatibilidad, mantenimiento e impacto.
- Usá TypeScript estricto; evitá `any` y conversiones inseguras. Tipá límites públicos, aprovechá inferencia interna y usá `readonly` donde corresponda.
- Mantené responsabilidades claras y nombres técnicos en inglés. Escribí comentarios útiles y descripciones de tests en español; evitá comentarios que repitan el código.
- Usá el framework de tests existente, con casos de comportamiento, errores y límites relevantes. No ocultes fallos cambiando expectativas ni abuses de mocks.
- Ejecutá primero verificaciones específicas; ampliá cuando el alcance lo justifique. Indicá qué verificaste y los límites de la evidencia.
- En proyectos del workspace personal, localizá y leé explícitamente su `AGENTS.md` de administración en los directorios padre, incluso si el proyecto tiene su propia raíz Git. Para checkouts externos, usá una ruta de contexto explícita con el acceso permitido; si no está disponible, informalo sin copiar documentación privada. Las reglas administrativas se mantienen allí y las técnicas específicas en cada repositorio.
- Preservá cambios previos. Usá ramas `feat/` o `fix/`. No hagas commit ni push sin pedido explícito; usá mensajes semánticos en español y estilo nominal.
- No despliegues ni ejecutes operaciones destructivas sin autorización. No instales configuración global ni sobrescribas archivos existentes sin autorización.
- Limitá este entorno a proyectos personales; no copies código, configuración o datos de empleadores. No versiones secretos ni los expongas en logs.
- Usá skills especializadas cuando correspondan y estén disponibles. Leé solo las referencias necesarias; evitá verificaciones repetidas y análisis completos para cambios triviales.
- No ejecutes subagentes por defecto ni delegues tareas triviales. Delegá solo ante un pedido o instrucciones aplicables que soliciten hacerlo; no asumas ahorro de tokens.
