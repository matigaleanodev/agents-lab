---
name: workspace-management
description: Consultar y mantener documentación operativa privada de proyectos en un workspace existente, incluyendo roadmaps, migraciones y handoffs. Usar para seguimiento significativo; no para documentación técnica pública ni resúmenes de cambios triviales.
---

# Documentación operativa del workspace

## Localizar y delimitar

Identificá el proyecto y su raíz Git. Localizá el workspace en los directorios padre del checkout y leé explícitamente su `AGENTS.md` de administración, incluso si el proyecto tiene un Git independiente. No deduzcas pertenencia solo por el nombre de una carpeta.

Para checkouts externos, usá la ruta de contexto indicada por el usuario o una configuración local ya existente que señale el workspace; no inventes claves de Codex ni una ruta absoluta pública. Verificá la asociación con el proyecto mediante sus instrucciones o referencias del workspace. Si falta ese contexto, pedilo antes de actualizar documentos. Si no hay acceso, informá la limitación sin crear, clonar ni copiar un workspace al proyecto.

Leé también el README del workspace y las instrucciones del proyecto. Comprobá estructura real, permisos de la sesión, raíces Git, estado e ignores de los destinos. No confundas un checkout anidado con contenido versionado por el workspace.

## Actualizar lo afectado

1. Buscá documentos del proyecto en las ubicaciones existentes. Según las políticas locales, priorizá `roadmap/` para planificación/progreso, `roadmap/archive/` para planes cerrados, `Docs/operations/` para operación, `Docs/handoffs/` para continuidad y `Docs/project-overviews/` para coordinación. Las instrucciones locales determinan ubicación, formato e idioma.
2. Seguí los enlaces del índice y el roadmap vigente hacia decisiones, contexto operativo o handoffs solo cuando ayuden al cambio. Leé el estado actual y contrastalo con evidencia de esta tarea. Diferenciá implementación, destino decidido e historial reemplazado; ante contradicciones, buscá la decisión que sustituye a la anterior y contrastá código/configuración. Si no se puede resolver, registrá la incertidumbre; autorizaciones históricas no autorizan acciones nuevas.
3. Determiná qué cambió realmente y editá solo los documentos afectados, reutilizando los existentes. Conservá historia y procedencia relevantes; no reorganices directorios ni generes todos los tipos de documento.
4. Registrá lo necesario para continuar: estado y pendientes de una funcionalidad; etapa, validaciones, riesgos, recuperación y próximos pasos de una migración; versión/commit, ambiente, resultado e incidentes de un despliegue autorizado. Para cerrar sesiones, registrá solo avances o bloqueos significativos.
5. Resolvé la raíz Git dueña desde el directorio del archivo, no solo desde el checkout inicial; comprobá tracking e ignores allí y en el workspace. Un archivo ignorado en un proyecto no pasa a ser automáticamente contenido del workspace. Revisá el diff y el tracking en esa raíz. Informá rutas modificadas, evidencia utilizada y pendientes; no dupliques el historial de Git ni registres resultados no confirmados.

## Límites

El `AGENTS.md` del workspace conserva las políticas administrativas, incluida clasificación pública/privada, idioma y preservación de fuentes; esta skill define el procedimiento y no lo modifica. Si se autoriza trasladar documentos, aplicá esas reglas antes de retirar originales y verificá copia y procedencia. No crees estructuras paralelas ni handoffs por cambios triviales.

Mantené la documentación privada en el workspace, fuera de Agent Lab y de repositorios públicos. No incorpores código fuente completo de proyectos, secretos, credenciales, `.env` sensibles ni información de empleadores. No leas valores secretos para documentar una operación.

Actualizar documentación no autoriza despliegues, operaciones remotas ni cambios en aplicaciones. No cambies `.gitignore` salvo necesidad explícita de la tarea y evaluación de su impacto; no hagas commits ni pushes automáticamente. Respetá el alcance autorizado para cada escritura, sin pedir de nuevo permisos ya otorgados.
