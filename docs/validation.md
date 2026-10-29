# Verificación

Separá formato, descubrimiento y comportamiento. Una skill válida puede tomar malas decisiones; un TOML parseable no demuestra que el cliente cargue el agente.

## Formato y referencias

Usá el `quick_validate.py` disponible dentro de la skill oficial `skill-creator` de tu cliente. Elegí un Python que ya tenga sus dependencias; si falta alguna, informalo antes de instalarla. Desde PowerShell, con las rutas reales en `$labPython` y `$labValidator`:

```powershell
$labRoot = (Get-Location).ProviderPath
$labSkills = @(Get-ChildItem -LiteralPath (Join-Path $labRoot '.agents/skills') -Directory -ErrorAction Stop |
    Where-Object { Test-Path -LiteralPath (Join-Path $_.FullName 'SKILL.md') -PathType Leaf } |
    Sort-Object Name)
$labAgents = @(Get-ChildItem -LiteralPath (Join-Path $labRoot '.codex/agents') -Filter '*.toml' -File -ErrorAction Stop |
    Sort-Object Name)
if (!$labSkills.Count -or !$labAgents.Count) { throw 'No se encontraron herramientas; revisá la raíz del repo.' }
foreach ($labSkill in $labSkills) {
    & $labPython $labValidator $labSkill.FullName
    if ($LASTEXITCODE -ne 0) { throw "Skill inválida: $($labSkill.Name)" }
}
# Usá $labSkills para revisar openai.yaml y $labAgents para parsear los TOML.
```

Validá además `agents/openai.yaml` con un parser YAML disponible, sintaxis de los TOML con `tomllib` (Python 3.11+) y existencia de enlaces locales. No descargues ni copies validadores al repo por costumbre.

Comprobá que los TOML incluyan `name`, `description` y `developer_instructions` no vacíos, con nombres únicos y sin campos de permisos que el esquema de agentes no admite. Verificá que `api-migration` pueda resolver su referencia a `cloud-api`.

Antes de publicar, revisá los archivos que Git incluiría y confirmá que `.local/` está ignorado con `git check-ignore .local/probe`. Una revisión de contenido es necesaria: `.gitignore` no garantiza ausencia de secretos.

## Descubrimiento sin tareas reales

Comprobá `codex --version` y las capacidades de esa instalación. Contrastá el catálogo con los nombres y rutas descubiertos en `$labSkills` y `$labAgents`; la existencia de archivos no prueba carga efectiva. Si el presupuesto del catálogo inicial omite entradas, diferenciá esa limitación de un fallo de carga y comprobá el selector o la invocación explícita. Verificá que nombres y rutas correspondan a las fuentes del laboratorio, no a otra copia instalada. Si validás Windows contra un checkout WSL, eso acredita el cliente Windows, no un cliente Ubuntu. Si no hay cliente en el host de destino, registrá esa limitación por separado de la copia y sus hashes.

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

Seleccioná unas pocas pruebas de mayor riesgo; la tabla es un catálogo de casos, no una ejecución obligatoria por herramienta. Para roles delegados, usá solo los autorizados; una lectura de sus instrucciones no es una prueba de comportamiento. Si probás `architect` o `implementer`, comprobá alcance, resultado y verificaciones. No ejecutes agentes adicionales solo por validar estructura. Las pruebas con modelo se realizan con una sesión autorizada y se reportan por separado de los chequeos estáticos.

## Simulación de instalación

Probá el bloque de instalación en una raíz descartable dentro de `.local/`, conservando el home personal. Comprobá que `-WhatIf` no escriba, que copie carpetas completas al quitarlo y que una colisión de skill o agente detenga toda la copia sin sobrescribir. Una carpeta sin `SKILL.md` y un directorio terminado en `.toml` no deben descubrirse. Repetí los casos con rutas que contengan espacios.

Guardá prompts, resultados y procedencia de las pruebas solo en `.local/` o en el destino privado que indiquen las instrucciones administrativas. Registrá por separado formato, descubrimiento y comportamiento, incluidos los casos que no se pudieron ejecutar.
