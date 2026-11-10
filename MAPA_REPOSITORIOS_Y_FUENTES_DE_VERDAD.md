# Repositorios y fuentes de verdad

## Repositorios WOSHealth

| Repositorio | Estado local | Fuente remota | Fuente operativa observada |
|---|---|---|---|
| `woshealth_back` | limpio, `ed1f490...`, branch `fix/proa-snc-1.3.1-input-state` | `babenza/woshealth_back` | jar activo M1 en Ubuntu |
| `woshealth_front_vue` | limpio, `2d98e29...` | `babenza/woshealth_front_vue` | no coincide con título servido en `:5182` |
| `woshealth_back_e2` | limpio, `9d63d95...`, `release/e2-mm17` | `babenza/woshealth_back_e2` | release `9d63d95-r98-mm29-20261106` |
| `woshealth_front_vue_e2` | limpio, `ea6dc0e...`, `release/e2-mm17` | `babenza/woshealth_front_vue_e2` | release `ea6dc0e-r98-mm29-20261106-identityfix` |
| `woshealth-m2-layer1` | limpio, `bec0c4a...`, sin upstream | remoto vacío | fuente preparada, no activada |
| `woshealth-docs` | `C:\Users\baben\Desktop\REPOSITORIOS\woshealth\woshealth-docs`, limpio, `f0f7ef0...` | no configurado | documentación de auditoría |

## Fuentes no Git

- `IntegracionModulo1`, `ContratoComun` y `Documentacion`: entregas/documentos; no son fuentes Git operativas.
- `C:\Users\baben\Desktop\REPOSITORIOS\herramientas`: toolchains compartidos y referencias de otros repositorios; se conserva como `REVIEW_BLOCKED`. Hay una referencia directa al Node portable desde `CORE-BUSINESS-OS` y un `pyvenv.cfg` que referencia Python 3.12 desde el árbol de QA; no existe prueba segura para migrar o eliminar este árbol.
- `woshealth\HERRAMIENTAS`: raíz canónica de evidencias, workspaces y artefactos WOSHealth.

La carpeta documental se movió desde `HERRAMIENTAS\workspace\woshealth-docs` a la ruta permanente indicada arriba. La ubicación anterior quedó eliminada y no hay referencias locales a ella.

## Worktrees

Las referencias M1 stale apuntan a rutas desaparecidas, pero sus ramas siguen existiendo y contienen commits no mergeados. Se preservaron ramas y se eliminaron únicamente referencias de worktree stale mediante Git.

Los worktrees E2 con cambios locales se conservaron intactos.
