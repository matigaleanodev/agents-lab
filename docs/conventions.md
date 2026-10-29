# Convenciones

Las preferencias portables están en [`instructions/AGENTS.md`](../instructions/AGENTS.md). Se integran al home de Codex; no incluyen rutas privadas ni instrucciones operativas de proyectos particulares.

## Límites de cada herramienta

- Angular e integración web: `angular-feature`, adaptada a la versión instalada.
- API nueva o mantenimiento con CDK: `cloud-api`.
- Migración conservando comportamiento: `api-migration`, con referencia a `cloud-api` para implementación serverless.
- Arquitectura compleja o revisión independiente: rol correspondiente, cuando se solicite delegación.

Las skills no instalan dependencias ni autorizan cambios externos por el hecho de ser invocadas. Las aprobaciones existentes siguen siendo válidas dentro de su alcance.

## Git

`main` es la base estable. El trabajo se realiza en ramas `feat/*` o `fix/*`; no se mantiene una rama `dev`.

Priorizá la menor cantidad razonable de commits por cambio coherente. Agrupá implementación, documentación y ajustes relacionados; evitá commits de avance o correcciones mecánicas separadas que no aporten una unidad útil de revisión. No mezcles objetivos independientes para reducir el conteo.

Escribí mensajes semánticos en español, con título nominal que describa el resultado y un cuerpo que explique los cambios principales, su motivo y las decisiones relevantes. Preferí integración por squash cuando una rama tenga varios commits y se solicite integrarla a `main`.

Esta convención es propia de Agent Lab; no cambia la política Git de los proyectos que utilicen sus herramientas.

## Backend y runtimes

Usá validación explícita, errores consistentes y logs útiles sin datos sensibles. Separá negocio de integraciones cuando aporte claridad; no impongas NestJS a handlers Lambda ni contenedores si no hacen falta.

Para Ionic, preferí Capacitor y plugins oficiales, sin incorporar Cordova. Para Angular Native, comprobá versión, runtime y madurez de APIs: no presupongas equivalencia con Angular web. Una funcionalidad nativa fuera del alcance de `angular-feature` necesita análisis específico en el proyecto.

## Documentación

La documentación de este laboratorio se escribe en español, con identificadores técnicos en inglés. Cada concepto tiene una fuente: las preferencias en instrucciones, los procedimientos en skills y los roles en TOML. Evitá duplicarlos.

El `AGENTS.md` de administración del Workspace privado define las reglas documentales y la ubicación del seguimiento. Consultalo cuando esté disponible; no reproduzcas sus reglas completas en este laboratorio. `.local/` queda reservado para temporales de pruebas y respaldos.
