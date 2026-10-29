# Agent Lab

Fuente de instrucciones y herramientas reutilizables para Codex en proyectos personales.

- Para proyectos del workspace personal, localizá y leé explícitamente su `AGENTS.md` de administración en los directorios padre, incluso con una raíz Git independiente. Para checkouts externos, usá la ruta de contexto proporcionada y el acceso permitido; si no está disponible, informalo sin copiar documentación privada al repo.
- Leé `docs/architecture.md` antes de cambiar la estructura o las rutas de instalación.
- Mantené las preferencias portables en `instructions/AGENTS.md`, los procedimientos en `.agents/skills/` y los roles en `.codex/agents/`.
- Este archivo gobierna este repositorio; no instala instrucciones globales.
- Conservá una base pequeña: sin build, dependencias ni scripts salvo una necesidad concreta.
- Escribí instrucciones y documentación en español; conservá identificadores técnicos en inglés.
- Documentá propósito, uso, configuración y límites vigentes; las reglas administrativas de documentación se mantienen en el workspace. `.local/` contiene temporales de pruebas y respaldos ignorados.
- No copies documentación privada, configuración personal completa, cuentas, credenciales ni datos de otros proyectos.
- No instales archivos fuera de este repositorio ni cambies configuración global sin autorización.
- Preservá archivos existentes. Las ramas nuevas usan `feat/` o `fix/`; commit, push y cambios remotos requieren pedido explícito.
- Usá `main` como base estable, sin `dev`. Agrupá cambios coherentes en pocos commits explicativos y seguí las convenciones Git de `docs/conventions.md`.
- Validá skills con el validador oficial disponible de `skill-creator`; comprobá TOML y descubrimiento con el cliente instalado. No confundas validación estática con una prueba de comportamiento.
- No ejecutes subagentes por defecto. Su uso requiere un pedido o instrucciones aplicables que soliciten delegación.
