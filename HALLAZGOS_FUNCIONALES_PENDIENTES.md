# Hallazgos funcionales pendientes

Estos puntos fueron observados, pero NO se modificaron en esta tarea:

1. `obtenerPacientePorId` puede escoger el primer tratamiento de un paciente.
2. La validación debe reforzar `decision_output` explícito.
3. Debe verificarse la correlación completa de runtime, engine, hashes y evaluación antes de mostrar recomendación.
4. El catálogo Git E2 `release/e2-mm17` no explica por sí solo el catálogo runtime `r98`.
5. El runtime E2 actual publica y ejecuta Tuberculosis aunque el objetivo documental indica cuatro módulos.
6. El puerto `5182` sirve una aplicación titulada Módulo 2 Capa 2, no la UI M1 esperada históricamente.
7. El backend directo `:8996` responde HTTP 500 en `/api/e2/m2/runs`, pero la ruta pública nginx responde HTTP 200; debe decidirse si se normaliza también el contrato interno.
8. SNC aparece bloqueado en M1; evidencia histórica del runner y el worker Tuberculosis requieren reconciliación.

## Evidencia de la segunda pasada de limpieza

9. El HTTP 500 directo de M2 E2 queda atribuido al desacuerdo `/api/e2/m2/runs` frente a `/api/m2/runs`; nginx lo oculta en la ruta pública, y el output root está presente.
10. Tuberculosis sigue siendo una fuente activa de E2: aparece en el catálogo `r98`, tiene bundle `R98/bundles/Tuberculosis` y worker vivo. No se eliminó ni se modificó.
11. La consolidación de `REPOSITORIOS\herramientas` queda bloqueada por consumidores externos identificados y falta de prueba de no uso.
