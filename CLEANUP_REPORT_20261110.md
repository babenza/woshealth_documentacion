# Cleanup report — 2026-11-10

## Alcance ejecutado

- Auditoría Git local y fetch remoto de los cinco repositorios WOSHealth.
- Auditoría Ubuntu de solo lectura.
- Auditoría HTTP de salud/catálogo/raíces.
- Creación de repositorio local de documentación bajo la raíz canónica.
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

Espacio liberado calculado por tamaños previos: `788155695` bytes, aproximadamente `0.73 GiB`.

## Preservado explícitamente

- Código fuente y ramas Git.
- Cambios sin commit de los worktrees M2 backend/frontend.
- ZIP de rollback no rastreado.
- `data`, `logs`, QA, bundles, extracciones, deliveries, outputs, backups y caches de contrato.
- `REPOSITORIOS\herramientas`, porque tiene consumidores externos y no es duplicado demostrado.

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
- Ubuntu/E2: servicios enabled/active; E2 root, health, runner y catálogo HTTP 200.
- E2 M2: HTTP 500; no se declara PASS funcional.
- Producción: raíz nginx y catálogo M1 respondieron HTTP 200; solo GET.
- HP-3: bloqueado por autenticación SSH.

## Flags

```text
CLEANUP_MASTER=FAIL
LOCAL_CLEANUP=PASS
HERRAMIENTAS_CONSOLIDATION=BLOCKED
GIT_AUDIT=PASS
GIT_SYNC=PASS
DOC_REPOSITORY=PASS
DOCUMENTATION=PASS
UBUNTU_AUDIT=PASS
UBUNTU_CLEANUP=BLOCKED
HP3_AUDIT=BLOCKED
HP3_CLEANUP=BLOCKED
E2_POSTCHECK=FAIL
PRODUCTION_UNTOUCHED=PASS
SECRETS_EXPOSURE_CHECK=PASS
CLINICAL_DATA_EXPOSURE_CHECK=PASS
FILESYSTEM_POLICY=PASS
```
