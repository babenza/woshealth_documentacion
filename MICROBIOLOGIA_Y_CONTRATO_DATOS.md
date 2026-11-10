# Microbiología y contrato de datos

## CURRENT observado

En Ubuntu existen `raw`, `prepared`, `processed_v29_clean_20260630`, `model_output_v27/v28/v29`, `mdro_layer2_inputs`, `mdro_layer2_outputs`, logs y un árbol de join M3. Existe un cron diario de correo de alertas, pero no se demostró un cron activo de inferencia.

## HISTORICAL

La cadena v29 documentada es launcher → `inferir_produccion_sin_reentrenar.R` → `core.R` → parches → `final_tables`. No se declaró vigente sin identificar su scheduler y consumidor.

## Contrato

La correspondencia RAW1/RAW9/RAW10/RAW11/RAW12/RAW13 queda como hipótesis histórica. No se encontró evidencia suficiente para elevarla a contrato actual sin comparar fichero de entrada, parser, transformación y consumidores.

No se copiaron datos clínicos ni se incluyeron muestras en documentación.
