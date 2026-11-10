# Operación y troubleshooting

## Comprobaciones seguras

```bash
systemctl is-enabled woshealth-e2-backend.service
systemctl is-active woshealth-e2-backend.service
curl -sS http://127.0.0.1:8996/api/e2/proa/health
curl -sS http://127.0.0.1:8996/api/e2/proa/catalog
curl -sS http://127.0.0.1:8792/health
```

## Resultado 2026-11-10

- E2 health: HTTP 200, `status=UP`, runner configurado y base accesible.
- Runner health: HTTP 200, cinco workers vivos.
- E2 catalog: `r98`, `production_approved=false`.
- M2 runs: HTTP 500, recurso no encontrado.
- HP-3: no autenticado.

No se usaron comandos de reinicio ni `sudo`.
