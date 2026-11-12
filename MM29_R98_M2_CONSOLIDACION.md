# Consolidación MM29/R98 y Módulo 2

Estado documental vigente de la campaña. Este documento no sustituye el
runbook de despliegue ni contiene datos clínicos, secretos o identificadores
de infraestructura.

## Estado de aceptación

- `M2_DAILY_PIPELINE_READINESS=PASS`.
- `M2_REAL_POSITIVE_MATCH_READINESS=NOT_OBSERVED_REAL_CASE`.
- `MASTER_GATE=PASS` (gate técnico/funcional E2; sin afirmar un positivo real).
- `READY_FOR_JUAN_VALIDATION=YES`.
- `JUAN_ACTION_REQUIRED=NONE`.

El circuito diario está operativo y validado. La observación de un caso MDRO
real con correspondencia M1 segura queda como evidencia clínica futura y no es
un requisito para validar la fixture sintética QA controlada.

## Arquitectura diaria demostrada

```mermaid
flowchart LR
  A[Laboratorio/Sclab] --> B[Descarga y anonimización Windows]
  B --> C[COMPLETA]
  C --> D[Bridge de entrada E2]
  D --> E[Preparación]
  E --> F[Capa 1 / R]
  F --> G[final_tables]
  G --> H[Capa 2]
  H --> I[Publicación atómica]
  I --> J[Correspondencia M1 segura, si existe]
  J --> K[PROA R98]
  I --> L[Monitor de alertas reales]
```

La tarea Windows funciona a las 09:00. E2 sondea cada 10 minutos, espera que
la entrada sea estable y compara un watermark de la colección de ficheros.
La hora exacta de descarga queda desacoplada del procesamiento posterior.
No se modificó la tarea Windows ni se solicitó ninguna credencial.

## Contrato RAW

- `RAW1`: `episodio_origen`, contexto de episodio añadido o calculado durante
  la anonimización para ingresados cuando está disponible.
- `RAW4`: código de paciente, conservado como identidad de paciente sin
  coerción.
- `RAW9`: fecha de muestra.
- `RAW10–15`: campos microbiológicos confirmados utilizados por el contrato.
- `RAW2` y `RAW3`: permanecen opacos; no se les asigna semántica autoritativa.
- Sclab no aporta un identificador hospitalario de petición; no se inventan
  `xid_peticion` ni `xpeticion_id`.

No se asignan tratamientos por paciente, fecha o medicación aislados.

## Identidad y correspondencia M1

Cuando exista una alerta MDRO real, el enlace M1 debe utilizar RAW4 más RAW1
validado, o una resolución estructurada inequívoca. No se utiliza la primera
coincidencia. Si no hay correspondencia, se conserva `MDRO_REAL=YES` y
`M1_MATCH=NO`. Si hay más de un candidato, el caso queda ambiguo y no se
enlaza automáticamente.

La correspondencia M1 no ejecuta acciones terapéuticas automáticas.

## Validación realizada

El run real publicado más reciente produjo:

- 185 aislados;
- 0 alertas MDRO;
- 0 aislados relevantes para alerta;
- 0 miembros de alerta.

El cero fue validado como resultado legítimo: Layer1 produjo `READY` y tablas
finales no vacías; Layer2 generó manifiesto, evaluación y artefactos completos;
la publicación fue atómica; el replay produjo hashes iguales. No fue un
dataset vacío, un fallo de R, un fallo de parser ni un fallo de Layer2.

## Operación y seguridad

- El bridge utiliza el recurso Windows ya disponible y su subruta de entrada
  autoritativa; no crea un fetcher paralelo ni nuevas credenciales.
- El watermark registra fichero detectado, huella de entrada, último run,
  outcome y timestamp.
- Un run incompleto no sustituye el run publicado anterior.
- El monitor de correo solo evalúa un run Layer2 publicado y con provenance
  real; no reacciona a un fichero nuevo, a Layer1 terminado, a pacientes M1 ni
  a fixtures.
- Producción permanece estrictamente read-only.

## R98 y validación pendiente

La evidencia funcional previa de R98 se conserva. La navegación browser del
caso real M2→M1→R98 no se presenta como caso clínico real: el UAT cerrado usa
la identidad sintética compartida `SYN-M1M2-MM29-R98-SHARED-20261111` y deja
visible la etiqueta de caso sintético.

## Evidencias

La trazabilidad completa requisito → implementación → validación → estado se
conserva en `HERRAMIENTAS/evidence/mm29-r98-20261106.md`. El bloque apto para
memoria se mantiene separado en `MEMORIA_CDTI_M2_DAILY_FLOW.md`.

## Cierre técnico E2 2026-11-11

Se publicó el ajuste de integración contextual M1↔M2 en
`origin/release/e2-mm17`: backend `34f0936` y frontend `96f76d3`. El enlace
visible usa paciente+episodio, conserva múltiples alertas M1 del mismo
episodio, muestra todos los aislamientos clasificados y no interpreta la
relación como causalidad tratamiento-cultivo.

La activación E2, el smoke de backend/frontend, el UAT de navegador, el
rollback al release previo y el restore al release nuevo fueron PASS. La
producción no se modificó.

El E2 accesible expone el run real de 185 y una fixture QA compartida. La
fixture fue creada en un directorio QA separado a partir de una salida generada
por la lógica M2, con claves comunes para M1/M2, casos MDRO y no-MDRO, varios
aislamientos, alertas múltiples y episodio distinto sin vínculo. El run real
no se modificó.

## Cierre QA E. coli y navegación persistente 2026-11-12

Se añadió una copia QA aislada `SYN-M1M2-MM29-R98-ECOLI-QA` sin modificar el
run compartido ni el run real. Contiene 9 aislamientos, incluye el caso
sintético `SYN-M1M2-CASE4-001`/`SYN-M1M2-CASE4-EP1` y verifica un antibiograma
estructurado con `S=AMOXICILLIN, CEFTRIAXONE`, `R=[]` e `I=[]`; los estados
vacíos se muestran como `Sin elementos`.

La navegación M2 → lista M1 → evaluación conserva paciente, episodio y
`runId` histórico. En R98 queda visible el aviso persistente de microbiología,
el aislamiento `ESCHERICHIA COLI`, sus valores S/R/I y la semántica de contexto
por paciente/episodio sin atribución causal. Commits frontend publicados en
`origin/release/e2-mm17`: `11a3acd`, `d61e83d`, `d0b72b7`. Backend vigente:
`1a780f0`.

La suite frontend completa permanece en `27 suites / 235 tests PASS`; las
pruebas backend focales M2 pasan. La suite backend completa en Windows no es
reproducible en este host porque los tests históricos de los ejecutores PROA
requieren un ejecutable `python` que no está instalado; no es un fallo del
código modificado. E2 quedó saludable tras el despliegue y producción sigue
intacta.
