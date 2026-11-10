# Alertas y BBDD

## M1 CURRENT

- SQL Server clínico: fuente de lectura.
- Consultas sobre vistas `imp.vh_pac_items`, `imp.vh_far_om`, `imp.vh_far_om_lin` y catálogo farmacológico.
- SQLite local: persistencia de evaluaciones validadas, requests/responses, versiones, hashes, identidad y decisiones profesionales.

## E2 CURRENT

- Backend E2 reporta `database_accessible=true`.
- La ruta M2 consultada no funcionó (`HTTP 500`), por lo que no se certifica la disponibilidad funcional del dataset.

## Seguridad

No se exportaron DTOs clínicos ni JSON clínicos. No se ejecutaron escrituras SQL ni acciones terapéuticas.
