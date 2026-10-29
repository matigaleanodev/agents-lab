# Skills

Las fuentes se encuentran en `.agents/skills/`, con nombres de carpeta iguales a `name` en el frontmatter de `SKILL.md`. Cada skill incluye metadatos de interfaz en `agents/openai.yaml`; no declara dependencias de herramientas ni desactiva la selección implícita.

| Skill | Activar para | No activar para |
| --- | --- | --- |
| `angular-feature` | Funcionalidades nuevas o cambios en Angular | Backend aislado o upgrade completo del framework |
| `cloud-api` | Implementación y mantenimiento de API con CDK | API ajena a CDK sin pedido de migración |
| `api-migration` | Migración de API existente a CDK por fases | API nueva o corrección aislada en CDK |
| `workspace-management` | Seguimiento operativo significativo en un workspace privado existente | Referencia técnica pública o resúmenes triviales |
| `github-actions` | Crear, revisar o diagnosticar workflows CI/CD | Implementar la aplicación u operar servicios remotos por defecto |
| `api-contract-testing` | Verificar contratos HTTP y comparar comportamientos | Tests internos sin HTTP o planificación completa de una migración |

`api-migration` referencia a `cloud-api` para la implementación serverless. Instalá ambas juntas; el enlace relativo conserva su destino si las carpetas siguen siendo hermanas.

Las nuevas skills no requieren dependencias adicionales: `workspace-management` necesita acceso al workspace y sus instrucciones, `github-actions` reutiliza workflows y validadores disponibles y `api-contract-testing` usa el framework del proyecto, con OpenAPI si existe. No crean un workspace ni instalan frameworks por defecto.

Para una migración, `api-contract-testing` aporta verificación concreta y `workspace-management` mantiene el seguimiento si corresponde; no repiten la planificación de `api-migration`. La administración documental sigue en el `AGENTS.md` del workspace. Ninguna skill autoriza despliegues, ejecuciones remotas, cambios de secretos o requests a producción; se respeta la autorización específica de cada operación.

## Descubrimiento y uso

Codex considera nombre y descripción antes de cargar instrucciones completas. Se puede solicitar cada skill como `$nombre`, por ejemplo `$github-actions`; también puede seleccionarla por la descripción. Seleccioná solo las necesarias para la tarea; no hay una cadena obligatoria de skills o agentes.

En CLI/IDE, usá el selector `$` o `/skills`; en Desktop, el selector de skills del cliente. Si una copia nueva no aparece, reiniciá el cliente. Evitá instalar una segunda copia del mismo nombre sin necesidad.

## Crear y actualizar

Usá `$skill-creator` con un procedimiento concreto, un alcance y ejemplos reales. Guardá el resultado en `.agents/skills/NAME/`. El formato mínimo es:

```yaml
---
name: example-skill
description: Procedimiento concreto y condición de uso.
---
```

Después escribí instrucciones útiles y proporcionadas. Usá `references/`, `assets/` o `scripts/` únicamente cuando resuelvan una necesidad; no copies manuales ni agregues scaffolding sin uso. `agents/openai.yaml` es opcional y sus campos deben coincidir con la skill. Los helpers oficiales de `skill-creator` pueden inicializarlo o generarlo.

Antes de actualizar una skill instalada, compará su contenido con la fuente, respaldá la copia y verificá que no tenga ajustes propios. Seguí [instalación](installation.md) y [verificación](validation.md). El validador oficial comprueba formato; las decisiones se evalúan con tareas representativas.

[Formato y mecanismos oficiales](https://learn.chatgpt.com/docs/build-skills).
