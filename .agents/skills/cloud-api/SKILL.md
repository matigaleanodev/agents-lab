---
name: cloud-api
description: Desarrollar o mantener APIs serverless con TypeScript, Node.js y AWS CDK v2, incluyendo handlers Lambda, contratos HTTP e infraestructura. Usar cuando el destino sea CDK; una migración de una API existente corresponde a api-migration.
---

# APIs serverless con CDK

## Contexto y diseño

Inspeccioná instrucciones, contratos, paquetes, runtime, estructura e infraestructura existentes. Respetá límites entre runtime e infraestructura, ambientes y convenciones. Si el proyecto usa otra herramienta de infraestructura y no se pidió migrarla, no la reemplaces silenciosamente.

Usá CDK v2 con TypeScript y Lambda/API Gateway cuando el pedido lo requiera. DynamoDB, Secrets Manager y otros servicios son opciones según el dominio, no requisitos. No impongas NestJS, contenedores ni una Lambda por endpoint o una función para toda la API sin analizar responsabilidades, permisos y empaquetado.

Si existen contratos compartidos, mantenelos neutrales: infraestructura puede consumir metadata y schemas sin importar handlers ni inicializar clientes runtime. Reutilizá npm workspaces, exports y lockfile únicos donde ya estén adoptados; no crees un paquete por Lambda ni migres la organización por rutina.

## Implementación

- Mantené handlers pequeños y contratos HTTP explícitos: método, ruta, autenticación, entrada, salida y errores. Separá negocio de integración AWS cuando aporte claridad.
- Validá entradas y normalizá errores con las soluciones existentes. Conservá coerciones, defaults y la capa responsable de validar; no traslades validación al gateway por rutina. Si Gateway y runtime seleccionan operaciones, verificá que métodos y rutas coincidan sin ampliar el acceso con rutas comodín. Centralizá respuestas solo si evita duplicación real.
- Revisá paquetes antes de agregar dependencias: solución disponible, compatibilidad, mantenimiento y efecto en bundle/carga. Justificá incorporaciones; no impongas Middy, Zod ni un framework de tests.
- Mantené infraestructura versionada, IAM mínimo por responsabilidad y configuración por ambiente. No inventes cuentas, perfiles, regiones o nombres de recursos.
- Usá variables de entorno para configuración y referencias a servicios de secretos cuando corresponda. No leas valores de secretos para auditar ni los copies al repo o logs.
- Conservá correlación útil en CloudWatch, con errores sanitizados. Revisá CORS, autenticación, exposición de recursos internos y límites de solicitudes según el acceso real.
- Verificá límites relevantes de la integración elegida: tamaño de payload y base64, timeout, memoria, concurrencia y dependencias nativas. No reduzcas contratos para ocultar incompatibilidades.
- En clientes HTTP externos, preservá cancelación/deadline, límites de tamaño, validación de respuestas y errores sanitizados. No agregues retries o redirects sin evaluar duplicación de efectos y presupuesto; reutilizá el cliente o SDK existente.
- Considerá costos de los recursos efectivamente propuestos; evitá servicios adicionales sin necesidad.

## Verificación

Ejecutá comandos existentes de typecheck, lint si existe, tests y build según el impacto. Cubrí contratos, errores y permisos relevantes; reutilizá el framework instalado y preferí Vitest cuando sea compatible y el proyecto lo adopte.

Inspeccioná la aplicación CDK antes de ejecutar `synth`: evitá lookups, resolución de secretos o efectos remotos en validación local. Validá la plantilla sintetizada y sus cambios de recursos, IAM y empaquetado. Un `cdk diff` puede consultar AWS y, según opciones/versión, crear un change set; preferí comparar plantillas locales y no lo clasifiques automáticamente como inocuo.

Los smoke tests deben tener destino y efectos explícitos. No uses producción ni integraciones reales si no están autorizadas. Una síntesis correcta no prueba el runtime ni sus integraciones.

## Operaciones AWS

No ejecutes deploy, bootstrap, creación, modificación o destrucción de recursos como verificación automática sin autorización. Antes de una mutación autorizada, verificá identidad con `aws sts get-caller-identity --profile PROFILE`, cuenta y rol esperados; usá perfil y región explícitos. Aplicá las reglas de acceso del proyecto, incluidas permission boundaries y roles de ejecución; no eludas sus restricciones mediante CI/CloudFormation ni eleves permisos después de un `AccessDenied`.

Entregá cambios, verificaciones y limitaciones concretas. Conservá evidencia operativa en archivos locales ignorados, no en documentación pública.
