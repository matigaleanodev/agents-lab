# Referencia de Codex

## Instrucciones y configuración

Codex lee `AGENTS.override.md` o `AGENTS.md` en su home y luego desde la raíz del proyecto hasta el directorio de trabajo; toma un archivo por directorio. Las instrucciones más específicas prevalecen. El límite combinado predeterminado es 32 KiB. El `AGENTS.md` de este repo no actúa como archivo global. [Documentación oficial](https://learn.chatgpt.com/docs/agent-configuration/agents-md).

La configuración personal reside en `$CODEX_HOME/config.toml` (por defecto `~/.codex/config.toml`). Las capas `.codex/config.toml` de proyecto requieren confianza; opciones CLI y capas más específicas pueden prevalecer, bajo las políticas administradas. Modelo, esfuerzo, proveedor y permisos son configuración del cliente. [Configuración oficial](https://learn.chatgpt.com/docs/config-file/config-basic).

## Skills

Una skill es una carpeta con `SKILL.md`, frontmatter YAML con `name` y `description`, e instrucciones. Puede incluir recursos y `agents/openai.yaml`. Codex carga primero metadatos y después el cuerpo cuando la selecciona, por coincidencia con la descripción o invocación explícita como `$cloud-api`.

Las rutas de autoría son `.agents/skills/` en el repo y `~/.agents/skills/` para el usuario. Existen skills de sistema y administración. Nombres duplicados no se fusionan. La instalación propia del cliente puede tener rutas adicionales; no copies su directorio completo.

`$skill-creator` crea skills y sus utilidades locales pueden validarlas. `$skill-installer` instala skills curadas o desde repositorios. Para distribuir como producto reutilizable, la documentación recomienda plugins; este laboratorio mantiene archivos para uso personal. [Skills oficiales](https://learn.chatgpt.com/docs/build-skills).

## Agentes

Los clientes locales actuales admiten archivos TOML independientes en `.codex/agents/` o `$CODEX_HOME/agents/`, con `name`, `description` y `developer_instructions`. Pueden fijar modelo, esfuerzo, resumen, verbosidad y desactivar capacidades admitidas; Agent Lab conserva herencia del padre.

Delegar crea otro contexto y consume trabajo adicional. Requiere un pedido o instrucciones aplicables que soliciten delegación. Los agentes heredan permisos, proveedor y MCP; un campo de sandbox dentro de su TOML no crea permisos propios. [Subagentes y esquema oficial](https://learn.chatgpt.com/docs/agent-configuration/subagents).

## Datos del cliente Desktop

El home de Codex contiene configuración, instrucciones, skills y datos locales del cliente, como autenticación, sesiones, cachés, logs y bases de estado. Estos datos no son una fuente portable de configuración para publicar. No versiones ni copies `auth.json`, sesiones, bases de datos o archivos de estado de la aplicación.

Windows y WSL pueden usar homes distintos. Confirmá el host del cliente que ejecuta Codex; abrir un proyecto por una ruta WSL no determina por sí solo dónde instalar las herramientas. Las ubicaciones relevantes para instalar están en la [guía de instalación](installation.md); los detalles internos de almacenamiento no son un contrato estable de Agent Lab.
