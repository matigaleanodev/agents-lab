---
name: api-contract-testing
description: Verificar contratos HTTP y detectar regresiones o incompatibilidades entre implementaciones de APIs, con el framework de tests existente. Usar para cambios públicos y comparación de comportamientos; no para pruebas internas sin contrato HTTP ni planificación completa de migraciones.
---

# Verificación de contratos HTTP

## Descubrimiento

Identificá endpoints, consumidores conocidos, restricciones y tests existentes. Usá OpenAPI si existe; en su ausencia, contrastá implementación, tests, documentación y expectativas de consumidores. Señalá contradicciones o información faltante; no inventes contratos ni exijas una especificación nueva.

Delimitá métodos, rutas, parámetros, headers, autenticación/autorización, validaciones y cuerpos de entrada/salida, códigos HTTP y errores esperados. En Node.js, NestJS, Lambda o API Gateway, identificá la capa observada: invocar un handler no verifica por sí solo routing, authorizers, CORS ni serialización del gateway.

## Casos e implementación

Definí casos concretos por riesgo: éxito, errores esperados, entradas inválidas, límites, ausencia de credenciales, acceso a recursos de otro usuario y compatibilidad con consumidores, según el contrato real. Relacioná cada caso con una fuente y su resultado esperado.

Reutilizá el framework instalado, sea Vitest u otro; no agregues dependencias por costumbre. Implementá tests solo si la tarea autoriza ediciones. Usá fixtures representativas y datos locales descartables; mantené independencia entre casos cuando corresponda. Sustituí integraciones externas en su límite sin mockear la respuesta HTTP que se intenta verificar.

Comprobá valores y estructura relevantes, headers y serialización, no solo el status o snapshots sin criterio. No cambies el contrato ni código productivo para hacer pasar tests sin autorización.

## Comparar implementaciones

Si hay dos versiones, ejecutá los mismos casos contra ambas dentro de entornos autorizados. Compará métodos/rutas, estados, headers, estructuras, errores y efectos observables que formen parte del contrato. Normalizá únicamente campos variables justificados, como identificadores o timestamps, sin ocultar diferencias semánticas.

Separá diferencias intencionales documentadas de regresiones y discrepancias sin decisión. La implementación original es evidencia de comportamiento, no garantía de corrección. No completes una matriz remota por inferencia si solo existe evidencia local.

## Validación y límites

Ejecutá pruebas locales y reportá casos/capas verificados, resultados, incompatibilidades, correcciones propuestas y pendientes. Una suite parcial no demuestra compatibilidad completa; un endpoint no se considera probado por haber escrito el test.

No ejecutes pruebas destructivas, modifiques datos productivos ni envíes requests a producción sin autorización explícita aplicable. Evitá credenciales reales innecesarias; para cualquier integración real, verificá destino y efectos autorizados antes de ejecutar.

Esta skill cubre verificación concreta y puede usarse sin migración. `api-migration` conserva la planificación por fases y la recuperación; `test-engineer` puede usar esta skill si está disponible, sin convertirla en dependencia obligatoria ni delegar automáticamente.
