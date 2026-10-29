# Verificación

Separá formato, descubrimiento y comportamiento. Una skill válida puede tomar malas decisiones; un TOML parseable no demuestra que el cliente cargue el agente.

## Formato y referencias

Usá el `quick_validate.py` disponible dentro de la skill oficial `skill-creator` de tu cliente. Elegí un Python que ya tenga sus dependencias; si falta alguna, informalo antes de instalarla. Desde PowerShell, con las rutas reales en `$labPython` y `$labValidator`:

```powershell
foreach ($labName in @('angular-feature', 'cloud-api', 'api-migration', 'workspace-management', 'github-actions', 'api-contract-testing')) {
    & $labPython $labValidator ".agents/skills/$labName"
    if ($LASTEXITCODE -ne 0) { throw "Skill inválida: $labName" }
}
```

Validá además `agents/openai.yaml` con un parser YAML disponible, sintaxis de los TOML con `tomllib` (Python 3.11+) y existencia de enlaces locales. No descargues ni copies validadores al repo por costumbre.

Comprobá que los TOML incluyan `name`, `description` y `developer_instructions` no vacíos, con nombres únicos y sin campos de permisos que el esquema de agentes no admite. Verificá que `api-migration` pueda resolver su referencia a `cloud-api`.

Antes de publicar, revisá los archivos que Git incluiría y confirmá que `.local/` está ignorado con `git check-ignore .local/probe`. Una revisión de contenido es necesaria: `.gitignore` no garantiza ausencia de secretos.

## Descubrimiento sin tareas reales

Comprobá `codex --version` y las capacidades de esa instalación. El catálogo debe reconocer las seis skills y los cinco agentes de este repo. Si el presupuesto del catálogo inicial omite entradas, diferenciá esa limitación de un fallo de carga y comprobá el selector o la invocación explícita. Verificá que nombres y rutas correspondan a las fuentes del laboratorio, no a otra copia instalada.

Cuando el cliente exponga `codex debug prompt-input`, podés inspeccionar el contexto construido sin ejecutar una tarea con modelo. Consultá primero `--help`; es una herramienta de diagnóstico dependiente de versión. Guardá cualquier salida solo en `.local/`: podría contener instrucciones privadas del entorno.

Para una comprobación aislada, usá un `CODEX_HOME` temporal dentro de `.local/` y restaurá la variable del proceso al finalizar. No copies `auth.json`, sesiones ni configuración privada. El home temporal no redirige por sí solo todas las fuentes de skills personales; diferenciá las herramientas del laboratorio del resto del catálogo.

## Comportamiento

En un proyecto descartable y con cambios autorizados, comprobá selección, resultado y límites usando estos casos:

| Pedido | Comportamiento esperado |
| --- | --- |
| Agregar un campo validado a un formulario Angular existente | `angular-feature`; inspeccionar versión, preservar API y probar el comportamiento afectado |
| Corregir un import trivial de Angular | Resolver con comprobación específica, sin análisis completo ni agentes |
| Agregar un endpoint en una API CDK existente | `cloud-api`; conservar patrones, validar contrato y sintetizar localmente si no hay efectos remotos |
| Relevar una API NestJS para migrarla | `api-migration`; inventario y riesgos, sin iniciar implementación ni desplegar |
| Corregir un endpoint CDK sin migración | `cloud-api`, sin activar un proceso completo de migración |
| Revisar cambios con `code-reviewer` por pedido explícito | Hallazgos concretos o ausencia de problemas; sin ediciones |
| Actualizar seguimiento de una migración con workspace disponible | `workspace-management`; localizar instrucciones y editar solo documentos afectados, sin copiar contenido privado al repo |
| Actualizar seguimiento con workspace inaccesible | Informar el límite; no crear, clonar ni copiar un workspace al checkout |
| Corregir un workflow CI existente | `github-actions`; conservar arquitectura, revisar permisos y condiciones, validar localmente sin disparar runs |
| Comparar errores HTTP de dos implementaciones locales | `api-contract-testing`; mismos casos, diferencias con evidencia y alcance de compatibilidad explícito |
| Revisar autenticación con `security-reviewer` por pedido explícito | Riesgos concretos y ubicaciones, distinguiendo evidencia e hipótesis; sin ediciones ni consultas de secretos |
| Diseñar estrategia con `test-engineer` por pedido explícito | Casos priorizados y límites; sin editar tests ni código productivo si solo se pidió análisis |
| Agregar un test de una funcionalidad común | El implementador usa el framework existente, sin delegar automáticamente en `test-engineer` |

Para los roles, probá también una decisión con `architect` y una implementación delimitada con `implementer`; comprobá alcance, resultado y verificaciones. No ejecutes agentes adicionales solo por validar estructura. Las pruebas con modelo se realizan con una sesión autorizada y se reportan por separado de los chequeos estáticos.
