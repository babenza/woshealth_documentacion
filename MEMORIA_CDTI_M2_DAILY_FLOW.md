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
