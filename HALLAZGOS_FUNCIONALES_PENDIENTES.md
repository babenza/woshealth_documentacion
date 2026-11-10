# Hallazgos funcionales pendientes

Estos puntos fueron observados, pero NO se modificaron en esta tarea:

1. `obtenerPacientePorId` puede escoger el primer tratamiento de un paciente.
2. La validación debe reforzar `decision_output` explícito.
3. Debe verificarse la correlación completa de runtime, engine, hashes y evaluación antes de mostrar recomendación.
4. El catálogo Git E2 `release/e2-mm17` no explica por sí solo el catálogo runtime `r98`.
5. El runtime E2 actual publica y ejecuta Tuberculosis aunque el objetivo documental indica cuatro módulos.
6. El puerto `5182` sirve una aplicación titulada Módulo 2 Capa 2, no la UI M1 esperada históricamente.
7. `/api/e2/m2/runs` responde HTTP 500.
8. SNC aparece bloqueado en M1; evidencia histórica del runner y el worker Tuberculosis requieren reconciliación.
