# Memoria CDTI — circuito diario M2

## Texto apto para memoria

El circuito operativo diario de microbiología ha sido validado con ficheros
reales. El flujo comprende la recepción diaria, la preparación de la entrada,
la ejecución de la Capa 1, la evaluación de la Capa 2 y la publicación atómica
de resultados validados.

La operación utiliza un mecanismo de estabilidad y watermark para desacoplar la
hora de recepción de la hora de procesamiento. La repetición del mismo lote es
idempotente y conserva la trazabilidad técnica desde la entrada hasta las
tablas finales y el manifiesto de salida.

Cuando existe correspondencia estructurada, la asociación con M1 utiliza el
paciente de origen y el episodio validado. Los casos sin correspondencia se
conservan sin enlazar y los casos ambiguos no se asocian automáticamente. No se
ejecutan acciones clínicas automáticas.

El circuito operativo diario ha sido validado con ficheros reales. En los lotes
reales utilizados durante la validación no se produjo una alerta MDRO positiva
con correspondencia simultánea en M1, por lo que la validación clínica
end-to-end de ese supuesto permanece condicionada a la aparición de un caso
real.

## Alcance

Este bloque está preparado para revisión e integración posterior. No se ha
insertado automáticamente en otro documento oficial y no contiene datos
identificativos, secretos ni detalles internos de infraestructura.

## Actualización técnica 2026-11-11

La publicación E2 de la integración M1↔M2 quedó versionada en backend
`34f0936` y frontend `96f76d3`, ambos en `origin/release/e2-mm17`. La interfaz
expone todos los aislamientos clasificados de la ejecución seleccionada y
calcula el contexto M1 por paciente y episodio, conservando los casos sin
correspondencia o sin episodio resoluble.

La activación, el smoke, el UAT de navegador, el rollback y el restore en E2
fueron satisfactorios. El run real contiene 185 aislamientos y la fixture QA
compartida permite reproducir la navegación M2→M1 con 4 vínculos, 2 alertas
M1 para el mismo episodio y un episodio distinto sin vínculo. No se observó un
positivo MDRO real ni se envió correo; `MASTER_GATE=PASS` se refiere al gate
técnico/funcional E2 y no a una afirmación clínica real.

## Actualización técnica 2026-11-12

La validación QA añadió el caso sintético E. coli
`SYN-M1M2-CASE4-001`/`SYN-M1M2-CASE4-EP1` en un run aislado. El contrato
estructurado conserva `S=AMOXICILLIN, CEFTRIAXONE`, `R=[]` e `I=[]`. En la
interfaz, los conjuntos vacíos confirmados conservan la etiqueta S/R/I con
contenido vacío; `No informado` solo representa un valor ausente o desconocido.
El contexto M1/M2
se conserva al pasar del histórico M2 a la lista M1 y a R98 mediante paciente,
episodio y `runId`, sin inferir causalidad tratamiento-cultivo.

La suite frontend completa pasó 235 tests. Las pruebas backend focales de
Módulo 2 pasaron; el conjunto backend completo mantiene un bloqueo ambiental
conocido en Windows por la ausencia del ejecutable `python` requerido por
tests históricos de ejecución PROA.

## Actualización técnica 2026-11-12 — etiquetas y contexto clínico

La presentación clínica no utiliza `sample_pk` ni `organism_pk` como nombres.
La fuente Layer1 conserva el linaje `muestra_label` → `sample_type_model` y
`germen_label_original`/`germen_label` → `germen_normalized`; Layer2 propaga
`sample_type` y `organism_normalized` cuando están disponibles. El backend y
la UI mantienen estos valores separados de las claves técnicas y aplican un
fallback explícito `No disponible`.

En M1 el aviso de microbiología permanece fuera del iframe de R98 y se repite
por cada aislamiento, con muestra, microorganismo, fecha, S/R/I y clasificación
MDRO. La asociación se limita al contexto paciente+episodio y no atribuye
causalidad al tratamiento. La prueba QA debe exponer en la lista M1 el caso
NO-MDRO y el caso MDRO como sintéticos, con navegación M1↔M2 y retorno estable.

## Actualización funcional 2026-11-13 — contexto microbiológico por defecto

La presentación M1 muestra ahora por defecto una tarjeta compacta expandida
para cada aislamiento. Incluye microorganismo, muestra, fecha, clasificación
MDRO/no-MDRO y S/R/I sin exigir la apertura de un enlace de evidencia. La
trazabilidad técnica queda secundaria y la redacción principal es clínica.
La tarjeta se conserva antes, durante y después de R98, al volver atrás, al
modificar el tratamiento y en la reevaluación; la relación sigue siendo
contextual y no causal.

La explicación funcional completa, separando recepción, Capa 1, Capa 2,
responsabilidad del aviso, papel web, papel profesional, asociación M1 y
causalidad terapéutica, queda en
`MEMORIA_M2_FUNCTIONAL_EXPLANATION.md`.

## Actualización técnica 2026-11-13 — determinismo temporal

El único fallo backend sensible a la fecha quedó reproducido y corregido sin
modificar la lógica clínica ni la selección operativa. Las pruebas inyectan un
reloj controlable en `M2DatasetService`; el comportamiento de producto conserva
el reloj de operación `Europe/Madrid`. La matriz cubre el mismo día, múltiples
ejecuciones, días anteriores, históricos y transiciones de día, mes, año y
UTC→Europe/Madrid.

La suite backend completa quedó en `201 tests, 0 failures, 0 errors, 15
skipped`. La explicación funcional de este documento y de
`MEMORIA_M2_FUNCTIONAL_EXPLANATION.md` permanece sin cambios de alcance.
