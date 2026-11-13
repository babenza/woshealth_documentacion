# Funcionamiento funcional del Módulo 2 de Microbiología e integración con Módulo 1

La línea base funcional desarrollada durante agosto de 2026 dejó disponible la
integración modular para seleccionar candidatos, recoger la información de
revisión y presentar resultados de forma segura. La evidencia consultada no
permite fijar un día exacto de cierre: permanece `PENDIENTE_DE_CONFIRMAR`.
El estado actual es una evolución posterior con circuito diario de Módulo 2,
Capa 1 y Capa 2, y presentación contextual M1↔M2 en MM29/R98. La documentación
técnica identifica la fuente/runtime de Capa 1 como v29/V26; esa referencia no
debe confundirse con el estado de campaña MM29/R98 de la aplicación web.

Cada ciclo recibe ficheros de microbiología anonimizados, estabiliza el lote y
prepara una entrada estructurada para su procesamiento periódico. El circuito
conserva watermark, idempotencia y trazabilidad, y publica el resultado
validado de forma atómica. La repetición de un lote no crea una segunda
interpretación clínica ni sustituye un resultado válido por uno incompleto.

La Capa 1 interpreta la información microbiológica y los antibiogramas,
normaliza muestras, microorganismos y sensibilidades, y estructura los datos
para la siguiente capa. Puede aplicar los modelos o reglas que formen parte del
runtime recibido, pero no asigna por sí sola un diagnóstico ni prescribe un
tratamiento. Su salida conserva el vínculo con la muestra y el organismo de
origen.

La Capa 2 consume esa salida estructurada, evalúa los criterios de alerta
microbiológica —incluida la clasificación MDRO— y conserva también los
aislamientos que no generan alerta. Es la capa que organiza y clasifica el
aviso microbiológico para su consulta; la interfaz web no crea la alerta ni
reimplementa la lógica microbiológica. Todas las salidas se presentan con
trazabilidad suficiente para revisar su procedencia.

La aplicación web muestra el contexto del episodio: microorganismo, tipo de
muestra, fecha, clasificación MDRO o no-MDRO y los valores S/R/I. La tarjeta
clínica se muestra expandida por defecto y los identificadores técnicos quedan
en una sección secundaria. El contexto permanece visible al entrar en R98,
volver atrás, modificar el tratamiento y realizar una segunda evaluación.

La interpretación clínica corresponde al profesional. El profesional decide
si el aislamiento es relevante para el episodio, confirma o descarta su
utilidad, integra el resto de la información asistencial y, cuando proceda,
valora un posible brote conforme al procedimiento clínico. El sistema no
confirma automáticamente un brote ni convierte una clasificación técnica en
una decisión terapéutica.

La asociación con Módulo 1 solo se realiza cuando existe correspondencia
estructurada de paciente y episodio. Los casos sin correspondencia se
conservan sin enlace y los casos ambiguos no se fuerzan. Puede haber varios
aislamientos o varias alertas para el mismo episodio. La navegación M1↔M2
permite abrir el aislamiento exacto y regresar conservando el contexto, sin
usar nombres, medicación o aproximaciones como sustitutos de la identidad
asistencial.

La microbiología es contexto compartido, no una inferencia de causalidad entre
cultivo y tratamiento. Un resultado S/R/I o una alerta MDRO no modifica por sí
solo la pauta ni determina una prescripción. Durante R98 el profesional
recibe ese contexto para revisar el caso, mientras que el bundle ejecuta su
contrato, preguntas y confirmaciones declaradas; la información microbiológica
no se convierte automáticamente en una variable clínica implícita del bundle.

La recepción, normalización, clasificación, asociación estructurada y
presentación son operaciones automatizadas del circuito técnico. La relevancia
clínica, la decisión sobre el tratamiento, la confirmación profesional y la
valoración de un brote son acciones del usuario autorizado. No se ejecutan
acciones terapéuticas automáticas.

Respecto de la versión disponible en agosto, la evidencia solo permite afirmar
una evolución posterior: se incorporaron el circuito diario de Módulo 2 y sus
capas, la normalización y trazabilidad microbiológica, la asociación M1↔M2 y
la presentación persistente durante R98. Las entregas R89/R91/R98 y la
expansión posterior de bundles forman parte de esa evolución; no deben
atribuirse como capacidades cerradas en agosto. La fecha exacta de cierre de
la línea base sigue pendiente de confirmación documental.
