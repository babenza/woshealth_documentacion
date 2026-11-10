# Módulo 2 — Capa 2

## Cadena observada

```mermaid
flowchart LR
  I[/mnt/pasados/microbiology/mdro_layer2_inputs/] --> P[mdro-layer2-vue/server.js]
  P --> O[/mnt/pasados/microbiology/mdro_layer2_outputs/]
  O --> V[public/dist run_manifest y CSV]
  V --> F[Frontend Capa 2]
  E[E2 backend] --> O
```

## CURRENT

- Proceso Node activo: `/home/suryka/modulo2/mdro-layer2-vue/server.js` en `:5182`.
- Se localizaron `public/data/run_manifest.json` y `dist/data/run_manifest.json`.
- La API E2 `/api/e2/m2/runs` devolvió HTTP 500 con `No static resource`.
- No se confirmó que la ruta histórica `/home/suryka/modulo2/mdro-layer2-vue` sea la fuente Git activa.

## Contrato

El código local define archivos por run, miembros, aislamientos, calidad, trazabilidad y claves `treatment_instance`/`idFarmaco`. La asociación no debe basarse en paciente o medicamento solos.
