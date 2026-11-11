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
11. `REPOSITORIOS\herramientas` queda clasificado como toolchain global compartido intencional; no contiene artefactos operativos WOSHealth demostrados.

## Clasificación para tareas independientes

12. `M2_ROUTE_CONTRACT_FINDING=FUNCTIONAL_TECHNICAL_DEBT`: el backend directo y el encaminamiento público usan prefijos distintos; la ruta pública funciona. Próxima tarea: añadir pruebas de contrato para backend directo y nginx, verificar `GET /api/e2/m2/runs` y `/api/m2/runs`, y normalizar un único prefijo sin modificar producción durante esta tarea.
13. `TUBERCULOSIS_SCOPE_FINDING=FUNCTIONAL_CONFIGURATION_MISMATCH`: r98 publica cinco módulos aunque el objetivo declarado contiene exactamente cuatro. Próxima tarea: confirmar el catálogo autorizado y ajustar de forma coordinada catálogo, runner, frontend y pruebas; no retirar bundle, worker, registro ni UI durante la limpieza.

## Actualización E2 2026-11-11

14. `M2_CONTEXT_LINK_FINDING=IMPLEMENTED_PATIENT_EPISODE`: el enlace
    contextual M1↔M2 ya no usa tratamiento/fármaco como clave y muestra todos
    los aislamientos clasificados.
15. `M2_FIXTURE_IDENTITY_FINDING=RESOLVED_SHARED_QA`: se creó en E2/QA una
    única fixture sintética compartida `SYN-M1M2-MM29-R98-SHARED-20261111`.
    Sus claves estructuradas paciente+episodio son comunes a M1/M2 y cubren
    MDRO, no-MDRO, múltiples aislamientos, múltiples alertas y episodio
    distinto sin vínculo. El run real 185 no se modificó.
