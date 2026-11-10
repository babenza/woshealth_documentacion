# Cleanup report — 2026-11-10

## Alcance ejecutado

- Auditoría Git local y fetch remoto de los cinco repositorios WOSHealth.
- Auditoría Ubuntu de solo lectura.
- Auditoría HTTP de salud/catálogo/raíces.
- Creación de repositorio local de documentación bajo la raíz canónica.
- Traslado de `woshealth-docs` a `C:\Users\baben\Desktop\REPOSITORIOS\woshealth\woshealth-docs` como ubicación permanente.
- Segunda pasada de limpieza local con comparación/hash antes de eliminar duplicados demostrados.
- Poda exclusivamente de metadata Git stale, tras conservar ramas y commits.
- Limpieza local limitada a artefactos regenerables explícitamente identificados.
- Fetch remoto correcto en los cinco repositorios WOSHealth.

## Eliminaciones locales demostradas

- `woshealth_back/target`.
- `woshealth_back_e2/build` y `woshealth_back_e2/target`.
- `woshealth_front_vue/dist` y `node_modules`.
- `woshealth_front_vue_e2/dist` y `node_modules`.
- `HERRAMIENTAS/worktrees/m2-layer2-backend/target`.
- `HERRAMIENTAS/worktrees/m2-layer2-frontend/dist` y `node_modules`.
- `HERRAMIENTAS/workspace/mm4-activation/rollback-mm3-m2-baseline/dist`.
- `HERRAMIENTAS/cache/maven-r74-20261029`.

## Segunda pasada: eliminaciones demostradas

- Duplicado exacto de `HERRAMIENTAS/workspace/integration/IntegracionModulo1`: se conservaron cuatro ficheros únicos en `HERRAMIENTAS/workspace/preserved/IntegracionModulo1-unique-20261110` y se eliminaron 92 ficheros duplicados, `211870240` bytes.
- Cuatro copias exactas de ZIP en la raíz de `ContratoComun` se eliminaron; se conservaron las copias de `ContratoComun/Evolucion2`, `89569171` bytes.
- Wrapper `Respiratorias/v5/proa_respiratorias_app_bundle_2_5_6_v9 (2).zip` se eliminó; su ZIP anidado coincide por SHA-256 con el V9 canónico, `826740` bytes.
- Total de esta pasada: `302266151` bytes, aproximadamente `0.28 GiB`.

Espacio liberado calculado por tamaños previos: `788155695` bytes, aproximadamente `0.73 GiB`.

## Preservado explícitamente

- Código fuente y ramas Git.
- Cambios sin commit de los worktrees M2 backend/frontend.
- ZIP de rollback no rastreado.
- `data`, `logs`, QA, bundles, extracciones, deliveries, outputs, backups y caches de contrato.
- `REPOSITORIOS\herramientas` se conserva intacto como conjunto de toolchains globales compartidos. La clasificación final es intencional, no un bloqueo: `WOSHEALTH_OPERATIONAL_ARTIFACTS_CONSOLIDATED=PASS` y `EXTERNAL_SHARED_TOOLCHAINS=INTENTIONAL`.
- Los releases y árboles remotos de Ubuntu siguen intactos porque no se demostró un candidato seguro de eliminación. Un `target` de incoming se conservó al estar referenciado por el `manifest.txt` de un release. Esto se clasifica como `UBUNTU_CLEANUP=PASS` con `UBUNTU_DELETIONS=NONE_REQUIRED`, no como bloqueo.

## No ejecutado

- HP-3: autenticación rechazada.
- Limpieza remota: no se eliminó nada en Ubuntu ni HP-3.
- Producción: no se modificó.
- Cambios funcionales, commits de aplicación y despliegues: no realizados.

## Estado final

Los elementos históricos de Respiratorias, ContratoComun, microbiología, releases, backups y outputs se preservan mientras no exista prueba de que son redundantes y no operativos.

## Postcheck final

- Raíces de los cinco repositorios de aplicación: limpias y alineadas con sus upstream cuando existe upstream.
- Worktrees E2 con cambios y rollback: preservados y sin publicación.
- Referencias stale M1: podadas con `git worktree prune`; ramas y commits conservados.
- Ubuntu/E2: servicios enabled/active; E2 root, health, runner y catálogo HTTP 200. No había eliminaciones seguras necesarias.
- E2 M2: el backend directo devuelve HTTP 500 en el prefijo no normalizado, pero la ruta pública nginx consumida por E2 devuelve HTTP 200; no se clasifica como caída.
- Producción: raíz nginx y catálogo M1 respondieron HTTP 200; solo GET.
- HP-3: bloqueado por autenticación SSH.
- M2 E2: el backend directo conserva HTTP 500 por desacuerdo de prefijos (`/api/e2/m2/runs` frente a `/api/m2/runs`), mientras la ruta pública nginx responde HTTP 200; queda pendiente normalizar el contrato interno.
- Tuberculosis E2: fuente activa documentada; no se trató como residuo histórico.

## Flags

```text
CLEANUP_MASTER=BLOCKED
LOCAL_CLEANUP=PASS
WOSHEALTH_OPERATIONAL_ARTIFACTS_CONSOLIDATED=PASS
EXTERNAL_SHARED_TOOLCHAINS=INTENTIONAL
HERRAMIENTAS_CONSOLIDATION=PASS
GIT_AUDIT=PASS
GIT_SYNC=PASS
DOC_REPOSITORY=PASS
DOCUMENTATION=PASS
UBUNTU_AUDIT=PASS
UBUNTU_CLEANUP=PASS
HP3_AUDIT=BLOCKED
HP3_CLEANUP=BLOCKED
E2_POSTCHECK=PASS
M2_E2_DIAGNOSIS=PASS
DOC_REPOSITORY_LOCATION=PASS
DOCUMENTATION_PUSH=BLOCKED
UBUNTU_DELETIONS=NONE_REQUIRED
M2_ROUTE_CONTRACT_FINDING=FUNCTIONAL_TECHNICAL_DEBT
TUBERCULOSIS_SCOPE_FINDING=FUNCTIONAL_CONFIGURATION_MISMATCH
PRODUCTION_UNTOUCHED=PASS
SECRETS_EXPOSURE_CHECK=PASS
CLINICAL_DATA_EXPOSURE_CHECK=PASS
FILESYSTEM_POLICY=PASS
```
