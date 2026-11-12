# Microbiología y contrato de datos

## CURRENT observado

En Ubuntu existen `raw`, `prepared`, `processed_v29_clean_20260630`, `model_output_v27/v28/v29`, `mdro_layer2_inputs`, `mdro_layer2_outputs`, logs y un árbol de join M3. Existe un cron diario de correo de alertas, pero no se demostró un cron activo de inferencia.

## HISTORICAL

La cadena v29 documentada es launcher → `inferir_produccion_sin_reentrenar.R` → `core.R` → parches → `final_tables`. No se declaró vigente sin identificar su scheduler y consumidor.

## Contrato

La correspondencia RAW1/RAW9/RAW10/RAW11/RAW12/RAW13 queda como hipótesis histórica. No se encontró evidencia suficiente para elevarla a contrato actual sin comparar fichero de entrada, parser, transformación y consumidores.

No se copiaron datos clínicos ni se incluyeron muestras en documentación.

## Linaje de etiquetas para M1↔M2

La fuente Layer1 `30c_mrsa_sri_runtime_tables_20260619.R` construye:

- `samples.sample_type_model` desde `muestra_label` y `comentario`;
- `organisms.germen_label_original`, `organisms.germen_label` y
  `organisms.germen_normalized` desde la salida de aislamiento;
- `antibiograms.germen_original` y `antibiograms.germen_normalized` para cada
  resultado S/R/I.

Los identificadores `sample_pk` y `organism_pk` son claves técnicas, no
etiquetas. El contrato de consumo M2 expone `sample_display_name` y
`organism_display_name` de forma aditiva, conserva las claves y no inventa una
etiqueta cuando el output no contiene el campo. `sample_type` y
`organism_normalized` son las columnas propagadas de Layer2 que pueden
resolver la presentación cuando el nombre Layer1 ya no está presente.

La interfaz M2 prioriza la etiqueta clínica y muestra las claves técnicas como
trazabilidad secundaria. El banner M1 mantiene la misma semántica por
aislamiento: fecha, microorganismo, muestra, S/R/I y MDRO/NO-MDRO; un contexto
compartido paciente+episodio no equivale a causalidad tratamiento-cultivo.
