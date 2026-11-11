# Monitor de alertas MDRO reales

## Objetivo

Avisar únicamente cuando un run real publicado de Layer2 contenga una alerta
MDRO procedente del circuito diario de laboratorio. El aviso informa de que ya
existe material real para completar la validación M2 → M1 → PROA R98.

## Contrato de disparo

No dispara el correo la existencia de un fichero nuevo, aislados, un fin de
Layer1, un fin de Layer2, pacientes M1 ni fixtures.

El monitor exige:

1. run publicado atómicamente;
2. manifiesto Layer2 válido;
3. manifiesto Layer1 listo;
4. provenance del feed real Windows;
5. `alerts > 0` y filas de alertas MDRO.

Se distinguen dos eventos:

- `REAL_MDRO_DETECTED`: alerta MDRO real sin correspondencia M1 segura.
- `REAL_MDRO_WITH_M1_MATCH`: alerta MDRO real con correspondencia M1 única y
  estructurada.

El segundo evento es el aviso prioritario para completar la validación
pendiente.

## Destinatarios y contenido

Destinatarios funcionales, sin añadidos:

- `babenza@wimaxonservices.es`;
- `juan@wimaxonservices.es`;
- `kiko@wimaxonservices.es`.

Asuntos:

- `WOSHealth E2 - Detectada alerta MDRO real`;
- `WOSHealth E2 - Caso real MDRO disponible para validar M2-M1`.

El cuerpo contiene solo evento, run, fecha de procesamiento y enlace funcional
a E2. No contiene nombre de paciente, DNI, historia clínica, comentarios
microbiológicos, tratamientos, secretos ni credenciales.

## Deduplicación y fallos

La clave de notificación es:

`published_run + source_record_id + event_type`

El estado solo avanza después de un envío SMTP correcto. Un fallo SMTP no
avanza el watermark. Un estado corrupto provoca fail-safe sin envío. Los casos
ambiguos no generan `REAL_MDRO_WITH_M1_MATCH`.

## Configuración segura

El servidor SMTP, puerto, remitente y contraseña se leen desde el mecanismo
protegido ya existente en E2. No se copian valores al repositorio, a logs ni a
la documentación. El contrato de destinatarios se valida antes del envío.

## Dry-run y validación

`--dry-run` renderiza evento, asunto y cuerpo sanitizado sin abrir conexión
SMTP. Se validaron:

- run real actual con cero alertas: no correo;
- MDRO sin M1: evento informativo en dry-run;
- MDRO con M1 único: evento prioritario en dry-run;
- evento repetido: no segundo aviso;
- correspondencia ambigua: no aviso prioritario;
- fallo SMTP: watermark intacto;
- estado corrupto: fail-safe;
- provenance sintética: sin correo.

No se envió correo de prueba a destinatarios reales.

## Operación y rollback

El monitor se ejecuta después de la publicación dentro del ciclo de polling
E2. Su rollback consiste en desactivar únicamente el monitor o retirar su
llamada del ciclo; el pipeline diario, su publicación y su watermark permanecen
independientes. El restore devuelve el monitor candidato a su estado anterior.

## Estado actual

`EMAIL_SENT=NO` y `REASON=NO_REAL_MDRO` para el run real disponible;
`M2_EMAIL_REAL_POSITIVE_READINESS=PASS`. La fixture QA sintética compartida no
dispara correo. El monitor queda preparado para el primer positivo real futuro
sin afirmar que exista uno.
