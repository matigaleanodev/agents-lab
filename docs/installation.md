# Instalación personal

Estos pasos modifican configuración fuera del repo: ejecutalos solo después de autorizar la instalación. La inicialización del laboratorio no los ejecuta. No hay instalador automático ni dependencias globales.

## Elegir alcance y host

| Fuente | Destino personal | Destino de un proyecto |
| --- | --- | --- |
| `instructions/AGENTS.md` | `$CODEX_HOME/AGENTS.md` | Integración manual en `AGENTS.md` |
| `.agents/skills/*` | `~/.agents/skills/` | `.agents/skills/` |
| `.codex/agents/*.toml` | `$CODEX_HOME/agents/` | `.codex/agents/` |

`CODEX_HOME` usa `~/.codex` por defecto; las skills personales usan el home del usuario, no se trasladan automáticamente al cambiar `CODEX_HOME`. Windows suele usar `$env:USERPROFILE` y WSL el home Linux. Elegí el host que ejecuta el cliente, aunque el repo viva en WSL. Revisá [rutas oficiales](codex-reference.md).

Abrir Agent Lab permite descubrir sus herramientas en ese proyecto. Para otros repos, elegí instalación personal o local; evitá duplicados del mismo nombre.

## Preparar y simular en PowerShell

Desde la raíz de Agent Lab, calculá las rutas sin escribir archivos:

```powershell
$labRoot = (Get-Location).ProviderPath
$labCodexHome = if ($env:CODEX_HOME) { $env:CODEX_HOME } else { Join-Path $env:USERPROFILE '.codex' }
$labSkillRoot = Join-Path $env:USERPROFILE '.agents/skills'
$labAgentRoot = Join-Path $labCodexHome 'agents'
$labNames = @('angular-feature', 'cloud-api', 'api-migration')

# Revisá todas las colisiones antes de copiar.
foreach ($labName in $labNames) {
    $labTarget = Join-Path $labSkillRoot $labName
    if (Test-Path -LiteralPath $labTarget) { throw "Ya existe: $labTarget; compará y respaldá antes de actualizar." }
}
foreach ($labFile in Get-ChildItem -LiteralPath (Join-Path $labRoot '.codex/agents') -Filter '*.toml') {
    $labTarget = Join-Path $labAgentRoot $labFile.Name
    if (Test-Path -LiteralPath $labTarget) { throw "Ya existe: $labTarget; compará y respaldá antes de actualizar." }
}

New-Item -ItemType Directory -Path $labSkillRoot,$labAgentRoot -Force -WhatIf
foreach ($labName in $labNames) {
    Copy-Item -LiteralPath (Join-Path $labRoot ".agents/skills/$labName") -Destination (Join-Path $labSkillRoot $labName) -Recurse -WhatIf
}
Get-ChildItem -LiteralPath (Join-Path $labRoot '.codex/agents') -Filter '*.toml' |
    ForEach-Object { Copy-Item -LiteralPath $_.FullName -Destination (Join-Path $labAgentRoot $_.Name) -WhatIf }
```

Con autorización y colisiones resueltas, repetí el bloque sin `-WhatIf`. La simulación muestra destinos; no prueba permisos efectivos ni valida el contenido. Instalá juntas las skills de migración y API.

## Instrucciones globales

Antes de editar `AGENTS.md`, revisá también `AGENTS.override.md`: puede tener prioridad. Respaldá el archivo global existente fuera del contenido publicable y compará con `instructions/AGENTS.md`. Integrá las preferencias manualmente sin duplicar reglas ni quitar restricciones existentes.

Si no existe el archivo, podés copiar la plantilla después de comprobar la ruta. No copies el `AGENTS.md` raíz del laboratorio como instrucciones globales: contiene reglas de mantenimiento propias del repo.

No hace falta reemplazar `config.toml`, fijar un modelo o habilitar permisos para estas herramientas. Si el cliente no soporta agentes independientes, seguí la alternativa de [agentes](agents.md).

## Actualizar

Obtené la revisión deseada del repo sin publicar cambios. Revisá el diff antes de sincronizar; la copia instalada puede tener modificaciones propias. Guardá un respaldo de cada ruta que vayas a reemplazar en un directorio privado, conservando la misma estructura, y anotá origen/destino en un registro local de instalación.

Con autorización para reemplazar, copiá las carpetas de skills completas y los TOML correspondientes. No copies la carpeta `.codex` entera ni el home personal. Para retirar archivos obsoletos, comprobá que pertenecen a la copia administrada y no contienen cambios propios; el reemplazo completo de una carpeta requiere la misma revisión y respaldo.

Mantené la integración global de `AGENTS.md` manual. No descargues helpers o dependencias globales como parte de actualizar contenido.

## Comprobar, restaurar y desinstalar

Reiniciá el cliente si no ve los cambios. Abrí un proyecto de prueba, comprobá skills y agentes según [verificación](validation.md) y pedí un resumen de las fuentes de instrucciones activas. Esa comprobación con modelo consume una interacción.

Para restaurar, compará con el respaldo, preservá cambios posteriores y recuperá solo las rutas de esa instalación. Si un archivo no existía antes, retiralo únicamente si sigue siendo la copia administrada.

Para desinstalar, revisá y retirá solo las tres carpetas de skills y los tres TOML registrados. Restaurá el global desde respaldo o quitá únicamente el bloque integrado, conservando el resto. Usá primero `Remove-Item -LiteralPath RUTA -Recurse -WhatIf` sobre cada ruta exacta; no borres raíces completas como `~/.agents` o `~/.codex`. El borrado real requiere autorización aplicable. No elimines autenticación, cachés ni sesiones.

## Herramientas oficiales

`$skill-creator` permite crear o ajustar skills y sus helpers validan formato. `$skill-installer` permite instalar desde repositorios; una vez publicados estos archivos, indicá `matigaleanodev/agents-lab` y las rutas `.agents/skills/...`. Comprobá el destino que el helper propone antes de autorizarlo. El instalador de skills no instala instrucciones globales ni agentes. No se necesita instalar nada desde GitHub para probar la copia local.
