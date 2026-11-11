# Entornos y despliegues

## Ubuntu `10.100.10.203` — CURRENT

- SSH validado como `suryka`.
- Disco raíz: 56G, 28G usados, 27G libres.
- `/mnt/pasados`: 447G, 435G usados, 12G libres; capacidad crítica.
- M1 backend activo en `:8986`.
- Frontend servido en `:5182` devuelve HTML titulado `Módulo 2 - Capa 2`.
- E2 backend activo en `:8996` y frontend en `:5192`.
- Nginx activo en `:80`.
- Servicios E2 enabled/active.

## E2 — CURRENT

- Catálogo HTTP: `r98`.
- `production_approved=false`.
- `automatic_action_allowed=false`.
- Backend activo: release `34f0936-mdro-status-20261111`.
- Frontend activo: release `9b50449-mm2-context-20261111`.
- Activación E2, smoke, rollback y restore verificados el 2026-11-11.
- UAT de navegador confirmó la vista de aislamientos, sus contadores y el
  contexto paciente/episodio.
- Cinco módulos publicados y cinco workers vivos: Respiratorias, Genitourinarias, Piel/Partes Blandas, Síndrome Febril y Tuberculosis.
- El objetivo documental indicado era exactamente cuatro módulos; la presencia de Tuberculosis es un conflicto activo, no se corrigió.
- El backend directo `:8996` respondió correctamente en health y en los
  endpoints M2 usados por el dashboard (`/api/m2/runs`, summary y links).
- El run real `20261111T165416Z` está disponible con 185 aislamientos y el
  contrato de cero alertas validado (`available=true`).
- La fixture QA compartida `SYN-M1M2-MM29-R98-SHARED-20261111` está disponible
  y fue validada por API y navegador con 8 aislamientos.

## Producción

La lectura de `:8986`, `:5182` y nginx se realizó sin POST, restart, deploy ni escritura. No se ejecutaron evaluaciones PROA.

## HP-3

El túnel `127.0.0.1:22200` escucha en Ubuntu, pero la autenticación SSH del usuario `bruno` fue rechazada con `Permission denied (publickey,password,keyboard-interactive)`. No hay agente SSH utilizable ni configuración SSH remota que aporte credenciales. Estado del host y tareas: `UNKNOWN / REVIEW_BLOCKED`.

Revisión final no interactiva: no apareció `ProxyJump`, `ProxyCommand`, `IdentityFile`, alias ni agente autorizado adicional. El bloqueo real es autenticación; la acción externa mínima es que un administrador proporcione una identidad SSH autorizada para `hp-3\bruno` o ejecute la auditoría con su acceso. No se cambiaron credenciales, ACL ni autenticación.

## Estado administrativo

- Ubuntu: auditoría completa y acceso operativo confirmados; no había eliminación segura justificada. `UBUNTU_DELETIONS=NONE_REQUIRED` y `UBUNTU_CLEANUP=PASS`.
- Documentación: `woshealth-docs` está en `main`, HEAD `668f342`, limpio y sin binarios. No hay remoto configurado. `DOCUMENTATION_PUSH=BLOCKED` porque no hay `gh`/`glab` disponible y el conector GitHub autenticado no tiene acceso al namespace de los remotos `babenza/*` ni un namespace autorizado para crear el repositorio privado.
