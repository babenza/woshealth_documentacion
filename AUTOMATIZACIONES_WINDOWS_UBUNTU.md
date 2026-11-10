# Automatizaciones Windows y Ubuntu

## Ubuntu CURRENT

- `woshealth-e2-backend.service`: enabled/active.
- `woshealth-e2-frontend.service`: enabled/active.
- `nginx.service`: enabled/active.
- Cron de usuario `suryka`: diario a las 08:00 para `script_email_alertas.py`.
- No se observaron timers relevantes en la salida filtrada.

## HP-3

`WOSHealth-E2-ReverseTunnel` y tareas programadas no pudieron auditarse porque el túnel SSH aceptó conexiones pero rechazó la autenticación de `bruno`. Estado `REVIEW_BLOCKED`.

No se deshabilitó ninguna tarea ni se reinició ningún servicio.
