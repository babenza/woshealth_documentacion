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

## Postcheck pendiente de cierre

El postcheck local se realizará sobre Git status, worktrees, documentación y ausencia de los targets eliminados. El postcheck remoto de HP-3 queda bloqueado por autenticación; Ubuntu/E2 se inspeccionó sin cambios.
