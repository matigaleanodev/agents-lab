---
name: api-migration
description: Migrar una API existente a AWS CDK conservando comportamiento, contratos y recuperación, desde relevamiento hasta preparación del cambio de tráfico. Usar para migraciones; para una API CDK nueva o mantenimiento aislado usar cloud-api.
---

# Migración de APIs hacia CDK

Trabajá en la fase solicitada; invocar esta skill no autoriza completar todas las fases ni desplegar. Mantené disponible la implementación anterior y preservá contratos. No agregues funcionalidades como parte de la migración.

## 1. Relevamiento

Inspeccioná API e infraestructura originales: framework, módulos, endpoints, autenticación/autorización, dependencias, integraciones, nombres de configuración, logging, tests y restricciones operativas. No copies valores de secretos.

Relevá contratos observables, incluyendo estados, headers, errores, formatos, payloads, autenticación, timeouts y efectos persistentes. Usá evidencia del código y tests; identificá incertidumbres sin inventar compatibilidad.

## 2. Plan

Proponé destino CDK, servicios necesarios, límites de responsabilidades y orden de fases. Evaluá riesgos, costos y diferencias de plataforma; verificá límites de payload, procesamiento y dependencias nativas antes de prometer equivalencia.

Definí estrategia de paridad, datos e integraciones, criterios de aceptación por fase y recuperación. Separá repositorios cuando el proyecto lo requiera; no lo impongas. Registrá plan y seguimiento en el espacio local ignorado del proyecto.

## 3. Implementación

Creá o reutilizá el destino según el alcance autorizado. Configurá TypeScript y CDK con las convenciones del proyecto, migrá negocio a handlers y conservá contratos. Definí configuración y referencias a secretos sin extraer valores privados.

Para implementar la API e infraestructura, consultá [cloud-api](../cloud-api/SKILL.md) cuando esté disponible; comparte los criterios serverless y de validación. Si no está instalada, aplicá la documentación del proyecto y la referencia oficial de CDK; no afirmes haberla ejecutado.

No alteres ni elimines la infraestructura anterior. No actives integraciones con efectos reales solo para completar tests.

## 4. Paridad y validación

Compará implementación original y destino mediante tests de contrato y casos representativos: éxito, errores, límites, autenticación y serialización. Incluí integraciones solo con entorno y efectos autorizados. No dupliques matrices ya cubiertas sin cambios relevantes.

Validá build, tests y plantilla CDK local con revisión de recursos y permisos. Prepará smoke tests con resultados esperados; el despliegue exitoso no demuestra paridad ni valida el cambio de tráfico.

## 5. Preparación del cambio productivo

Documentá como referencia técnica el procedimiento de despliegue, cambio de tráfico, comprobaciones posteriores y rollback. Para datos mutables, contemplá compatibilidad de escrituras, sincronización y reversión: volver el DNS no revierte datos.

Confirmá disponibilidad y recuperación del servicio anterior, criterios para abortar y permisos necesarios. Separá lo preparado de lo ejecutado.

La preparación no autoriza despliegues productivos, cambios de DNS, eliminación de recursos ni retiro del servicio anterior. Ejecutá esas acciones solo con autorización explícita aplicable y respetando la política AWS del proyecto. Informá evidencia, incertidumbres y el límite de la fase completada.
