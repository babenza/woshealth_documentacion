# Repositorios y fuentes de verdad

## Repositorios WOSHealth

| Repositorio | Estado local | Fuente remota | Fuente operativa observada |
|---|---|---|---|
| `woshealth_back` | limpio, `ed1f490...`, branch `fix/proa-snc-1.3.1-input-state` | `babenza/woshealth_back` | jar activo M1 en Ubuntu |
| `woshealth_front_vue` | limpio, `2d98e29...` | `babenza/woshealth_front_vue` | no coincide con título servido en `:5182` |
| `woshealth_back_e2` | limpio, `9d63d95...`, `release/e2-mm17` | `babenza/woshealth_back_e2` | release `9d63d95-r98-mm29-20261106` |
| `woshealth_front_vue_e2` | limpio, `ea6dc0e...`, `release/e2-mm17` | `babenza/woshealth_front_vue_e2` | release `ea6dc0e-r98-mm29-20261106-identityfix` |
| `woshealth-m2-layer1` | limpio, `bec0c4a...`, sin upstream | remoto vacío | fuente preparada, no activada |
| `woshealth-docs` | `C:\Users\baben\Desktop\REPOSITORIOS\woshealth\woshealth-docs`, limpio, `668f342...` | no configurado | documentación de auditoría |

## Fuentes no Git

- `IntegracionModulo1`, `ContratoComun` y `Documentacion`: entregas/documentos; no son fuentes Git operativas.
- `C:\Users\baben\Desktop\REPOSITORIOS\herramientas`: cinco instalaciones compartidas (`java`, `maven3.10`, `node`, `python`, `qa-tools`). Se clasifican como `GLOBAL_TOOLCHAIN` y se conservan intencionadamente fuera de WOSHealth: Node tiene consumidor directo en `CORE-BUSINESS-OS`, Python tiene consumidores en QA/E2 y PowerShell en las guías Windows E2. No quedan artefactos operativos WOSHealth demostrados fuera de la raíz canónica.
- `woshealth\HERRAMIENTAS`: raíz canónica de evidencias, workspaces y artefactos WOSHealth.

La carpeta documental se movió desde `HERRAMIENTAS\workspace\woshealth-docs` a la ruta permanente indicada arriba. La ubicación anterior quedó eliminada y no hay referencias locales a ella.

Clasificación final: `WOSHEALTH_OPERATIONAL_ARTIFACTS_CONSOLIDATED=PASS`; `EXTERNAL_SHARED_TOOLCHAINS=INTENTIONAL`.

## Worktrees

Las referencias M1 stale apuntan a rutas desaparecidas, pero sus ramas siguen existiendo y contienen commits no mergeados. Se preservaron ramas y se eliminaron únicamente referencias de worktree stale mediante Git.

Los worktrees E2 con cambios locales se conservaron intactos.
