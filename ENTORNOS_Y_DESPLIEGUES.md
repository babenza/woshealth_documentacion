# Entornos y despliegues

## Ubuntu `10.100.10.203` — CURRENT

- SSH validado como `suryka`.
- Disco raíz: 56G, 28G usados, 27G libres.
- `/mnt/pasados`: 447G, 435G usados, 12G libres; capacidad crítica.
- M1 backend activo en `:8986`.
- Frontend servido en `:5182` devuelve HTML titulado `Módulo 2 - Capa 2`.
- E2 backend activo en `:8996` y frontend en `:5192`.
- Nginx activo en `:80`.
- Servicios E2 enabled/active.

## E2 — CURRENT

- Catálogo HTTP: `r98`.
- `production_approved=false`.
- `automatic_action_allowed=false`.
- Cinco módulos publicados y cinco workers vivos: Respiratorias, Genitourinarias, Piel/Partes Blandas, Síndrome Febril y Tuberculosis.
- El objetivo documental indicado era exactamente cuatro módulos; la presencia de Tuberculosis es un conflicto activo, no se corrigió.
- En el backend directo `:8996`, `/api/e2/m2/runs` respondió HTTP 500 por recurso no encontrado y `/api/m2/runs` respondió HTTP 200. La causa demostrada es el desacuerdo de prefijos; no es una ausencia de `WOS_M2_OUTPUT_ROOT`.
- La ruta pública nginx `/api/e2/m2/runs` respondió HTTP 200 y devolvió runs disponibles, por lo que el smoke público queda correcto aunque el contrato directo del backend siga inconsistente. No se aplicó una corrección funcional en esta tarea.

## Producción

La lectura de `:8986`, `:5182` y nginx se realizó sin POST, restart, deploy ni escritura. No se ejecutaron evaluaciones PROA.

## HP-3

El túnel `127.0.0.1:22200` escucha en Ubuntu, pero la autenticación SSH del usuario `bruno` fue rechazada con `Permission denied (publickey,password,keyboard-interactive)`. No hay agente SSH utilizable ni configuración SSH remota que aporte credenciales. Estado del host y tareas: `UNKNOWN / REVIEW_BLOCKED`.
