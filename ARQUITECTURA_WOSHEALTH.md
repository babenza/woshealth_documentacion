# Arquitectura WOSHealth

## Estado actual observado

```mermaid
flowchart LR
  SQL[(SQL Server clínico<br/>read-only)] --> M1[Backend M1<br/>Spring Boot :8986]
  M1 --> S[(SQLite PROA local)]
  M1 --> R[Runner / bundles PROA]
  R --> M1
  E2UI[Frontend E2 :5192] --> E2[E2 backend :8996]
  E2 --> ER[Runner E2 :8792 local en Ubuntu]
  E2 --> M2O[/mnt/pasados/microbiology/<br/>Layer 2 outputs]
  C2[Frontend observado en :5182<br/>título Módulo 2 Capa 2] --> C2API[Backend/API asociado no resuelto]
```

## Separación

- **M1 CURRENT:** backend `woshealth_back`, frontend histórico `woshealth_front_vue`, backend activo en `:8986`.
- **E2 CURRENT:** release backend `9d63d95-r98-mm29-20261106`, frontend `ea6dc0e-r98-mm29-20261106-identityfix`.
- **M2 Capa 1:** fuente Git `woshealth-m2-layer1`, marcada no activada.
- **M2 Capa 2:** proceso Node en `/home/suryka/modulo2/mdro-layer2-vue`; la API E2 `/api/e2/m2/runs` respondió HTTP 500.
- **M3:** existe evidencia de pipelines/join en filesystem remoto, pero el servicio vigente no quedó identificado.

No se modificó lógica clínica ni funcional.
