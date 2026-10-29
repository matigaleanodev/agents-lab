# Arquitectura

Agent Lab administra archivos declarativos. No contiene aplicación, servicio, infraestructura desplegable ni herramientas de build.

## Separación

- `AGENTS.md`: mantenimiento del laboratorio.
- `instructions/AGENTS.md`: preferencias portables para integrar, con autorización, en el home de Codex.
- `.agents/skills/*/SKILL.md`: procedimientos especializados, con carga bajo demanda.
- `.codex/agents/*.toml`: roles con `name`, `description` y `developer_instructions`.
- `docs/`: referencia pública; `.local/`: evidencia privada y descartable.

Las rutas nativas permiten descubrimiento local sin duplicar archivos en `skills/` o `agents/`. La instalación personal copia archivos; no requiere enlaces simbólicos. El Workspace privado sigue siendo dueño de sus proyectos y de la operación de sus entornos.

## Alcance

Las instrucciones globales aportan preferencias; las de cada repositorio precisan contratos y procedimientos. Una skill describe cómo trabajar. Un agente define un rol delegado. El modelo y su esfuerzo son configuración del cliente, no una skill ni un reemplazo de permisos.

Los roles no fijan modelo, proveedor ni esfuerzo: heredan los del padre. Sus restricciones de edición son instrucciones de comportamiento, no un sandbox independiente. No se altera la configuración de seguridad para instalarlos.

No hay delegación automática ni promesas de ahorro de tokens. Cada agente añade su propio trabajo y contexto; usalo solo ante una necesidad concreta y un pedido de delegación.

Los contratos, nombres de recursos, regiones, cuentas y permisos se resuelven en el proyecto destino. No se transporta configuración operativa del Workspace.

## Mantenimiento

Agregá una skill cuando exista un procedimiento repetido; agregá un agente cuando exista una responsabilidad delegable distinta. No crees placeholders para herramientas futuras. Las nuevas capacidades deben incluir instrucciones, alcance y una forma de verificación proporcional.

Las rutas y formatos se apoyan en la [referencia oficial](codex-reference.md). No se usan tablas antiguas de registro de agentes ni campos de sandbox dentro de los roles.
