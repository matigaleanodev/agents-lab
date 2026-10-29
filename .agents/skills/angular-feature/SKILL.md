---
name: angular-feature
description: Implementar o modificar funcionalidades Angular existentes o nuevas, incluyendo componentes, estado, formularios, rutas e integración HTTP. Adaptar el trabajo a la versión y patrones reales del proyecto; no usar para una API backend ni para migraciones completas del framework.
---

# Funcionalidades Angular

## Inspección y alcance

Leé las instrucciones del repositorio, `package.json`, configuración Angular y archivos relacionados con el pedido. Identificá versiones, runtime, organización por funcionalidades, estilos, navegación y framework de tests. Inspeccioná consumidores y contratos afectados; reutilizá patrones y utilidades existentes.

Para un cambio trivial, resolvé directamente con una comprobación específica. Para funcionalidades con varias partes, delimitá comportamiento esperado y verificaciones antes de editar. No conviertas el pedido en una migración del código heredado.

## Implementación

- Preferí componentes standalone y servicios con responsabilidades claras, respetando compatibilidad y arquitectura del proyecto.
- Usá signals para estado y `computed()` para derivados; `inject()` para dependencias. Declaraciones `readonly` protegen la referencia, no impiden actualizar una writable signal.
- Usá `input()` y `output()` como `readonly` cuando la versión lo soporte. Reservá `private` para miembros internos que no necesite el template; evitá exponer estado mutable innecesariamente.
- Preferí `@if`, `@for`, `@switch` y `@let` cuando estén disponibles. Mantené templates simples, claves de seguimiento estables y pipes desde el template.
- En Angular web/Ionic, integrá APIs con `HttpClient`, tipos y manejo de errores coherentes con el repo. Evitá suscripciones manuales innecesarias y limpiá recursos según el ciclo de vida.
- Conservá el modelo de formularios y estado adoptado; usá formularios reactivos cuando correspondan, con validación, estados de carga/error y feedback accesible. Reutilizá servicios de página para coordinar flujos y servicios de dominio para validar/persistir cuando el proyecto ya los separe. Conservá rutas y contratos fuera del alcance.
- En Ionic, respetá Capacitor y los plugins oficiales existentes; no incorpores Cordova. En Angular Native, comprobá versiones de Angular, paquetes nativos y Expo, APIs y madurez en documentación oficial vigente antes de implementar. Usá componentes, eventos, accesibilidad y estilos del runtime nativo; no traslades DOM, APIs de navegador ni componentes Ionic por analogía. Conservá persistencia offline y su recuperación si existen; una actualización del framework es un alcance separado.

## Verificación y entrega

Usá el framework y comandos existentes; preferí Vitest si ya está adoptado. Cubrí comportamiento nuevo o corregido, errores y límites relevantes sin mocks excesivos. Ejecutá primero el caso afectado y luego typecheck, lint o build según el impacto.

Si cambia la interfaz, revisá labels, semántica, foco, teclado y estados de carga/error. Diferenciá comprobaciones automáticas de las pruebas visuales o de dispositivo que realmente ejecutaste.

Revisá el diff para eliminar cambios ajenos al pedido. Informá qué cambió, verificaciones y límites pendientes; no afirmes funcionamiento sin evidencia.
