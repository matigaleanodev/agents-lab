# Agent Lab

Configuración reutilizable de Codex para proyectos personales Angular y APIs con AWS CDK. Centraliza preferencias, procedimientos y roles para reducir instrucciones repetidas y decisiones inconsistentes.

Es independiente del Workspace privado: acá se versionan herramientas portables; cada proyecto conserva su arquitectura, contratos, recursos y documentación operativa.

## Organización

| Ruta | Responsabilidad |
| --- | --- |
| `AGENTS.md` | Reglas para trabajar en este repositorio |
| `instructions/AGENTS.md` | Plantilla de preferencias globales; requiere instalación explícita |
| `.agents/skills/` | Skills reconocibles dentro de este repo |
| `.codex/agents/` | Agentes locales, según soporte y confianza del cliente |
| `docs/` | Referencia de arquitectura, instalación y uso |
| `.local/` | Investigación y respaldos privados, ignorados por Git |

## Herramientas

| Skill | Uso |
| --- | --- |
| `angular-feature` | Implementar o modificar funcionalidades según la versión real de Angular |
| `cloud-api` | Desarrollar APIs serverless con TypeScript y AWS CDK v2 |
| `api-migration` | Migrar APIs a CDK conservando contratos, recuperación y servicio anterior |

| Agente | Uso |
| --- | --- |
| `architect` | Analizar decisiones complejas y alternativas |
| `implementer` | Implementar una tarea ya delimitada |
| `code-reviewer` | Revisar bugs, regresiones, seguridad y contratos |

Los agentes heredan modelo y permisos del padre. No se ejecutan por tener estos archivos y no se invocan para cada cambio.

## Uso

Abrí este repositorio como proyecto de Codex. Las skills de otro repo requieren [instalación](docs/installation.md).

```text
Usá $angular-feature para agregar filtros al listado existente, sin cambiar su API.
Usá $cloud-api para agregar GET /items con las convenciones y permisos del proyecto.
Usá $api-migration para relevar esta API y preparar la primera fase, sin desplegar.
Delegá en code-reviewer la revisión de esta rama contra main; no modifiques código.
```

La inicialización del repo no instala preferencias globales. Para instalarlas, actualizarlas, restaurarlas o desinstalarlas, seguí [instalación](docs/installation.md). Para extender y probar las herramientas, consultá [skills](docs/skills.md), [agentes](docs/agents.md) y [verificación](docs/validation.md).

[Arquitectura](docs/architecture.md) · [Convenciones](docs/conventions.md) · [Referencia oficial](docs/codex-reference.md)
