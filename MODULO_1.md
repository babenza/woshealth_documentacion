# Módulo 1

## CURRENT

Backend Spring Boot/Java 17 en `woshealth_back`; frontend Vue 3 en `woshealth_front_vue`. El backend activo expone catálogo M1 con Respiratorias `2.5.6`, engine `0.4.2-app-contract-patch2`, runtime `2.5.6`, Genitourinarias y SNC bloqueado.

## Flujo

SQL Server read-only → `PacienteAlertaDTO` → selección de módulo/regla → validación de bundle → runner → validación de salida → SQLite local → recomendación → decisión profesional separada.

## Identidad

La trazabilidad incluye paciente, capítulo, asistencia, orden, línea, fármaco y fechas. El endpoint por paciente puede devolver el primer tratamiento; queda documentado como hallazgo, no corregido.

## Endpoints

`/api/v1/alertas/pacientes`, `/api/v1/alertas/pacientes/{idPaciente}`, `/api/proa/modules`, `/api/proa/modules/{moduleId}/selection`, `/api/proa/evaluations` y decisión profesional.

`Modulo3AlertaBaseDTO` no forma parte de este flujo.
