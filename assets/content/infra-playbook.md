# Infra Playbook – Setup bis Prod

## 0. Prinzipien
- Keep it simple: API + Vector DB + Frontend. Erst danach fancy.
- Secrets nie im Repo; env-Dateien/Secret Manager.
- Logging ab Tag 1 (Requests, Tokens, Errors, Latenz).

## 1. Dev Setup (lokal)
- Python 3.11, `python -m venv .venv && source .venv/bin/activate`.
- Install: `pip install fastapi uvicorn openai anthropic chromadb tiktoken pydantic`.
- Start: `uvicorn app:app --reload --port 8000`.
- Lint/Format: `ruff`, `black` (optional).

## 2. Docker Build
- Base: `python:3.11-slim`.
- Multi-stage: builder (poetry/pip) → runtime (slim, non-root user).
- Healthcheck: `CMD curl -f http://localhost:8000/health || exit 1`.
- Example compose: FastAPI + Chroma + nginx.

## 3. VM Provisioning
- Cloud: Hetzner CX41 / AWS t3.xlarge für CPU; GPU: A10/A100/4090.
- OS: Ubuntu 22.04.
- Schritte:
  1. SSH Keys, `sudo apt update && sudo apt upgrade -y`.
  2. Docker: `curl -fsSL https://get.docker.com | sh`.
  3. Add user to docker group, relogin.
  4. `docker compose up -d` ausführen.

## 4. Networking
- Ports: 80/443 offen, 22 nur mit Keys.
- Reverse Proxy: nginx/Traefik, TLS via Let’s Encrypt.
- CORS konfigurieren, Rate Limits setzen.

## 5. Observability
- Logs: stdout zu Loki/CloudWatch.
- Metrics: Prometheus (latency, tokens, errors, cache-hits).
- Traces: OpenTelemetry optional.
- Alerts: UptimeRobot/Healthchecks + Slack/Discord Webhook.

## 6. Deploy Workflow
- Branching: main + feature branches.
- CI: Lint + tests + eval suite; docker build & push.
- CD: Deploy via compose/Ansible/Fly.io; migrations (if DB) vor App-Restart.

## 7. Cost Control
- Budget Alerts in Cloud; Autosleep für Dev-VMs.
- Token-Kosten tracken pro User/Feature.
- Caching (prompt + response) für Populäres.

## 8. Security
- Secrets in Vault/SM, nicht in Frontend bundeln.
- PII-Minimierung, Log-Redaction.
- Regelmäßige Updates (`unattended-upgrades`), Fail2ban/ufw.

## 9. DR/Backup
- Backups von Vector DB und App-Config (S3/Backblaze).
- Rollbacks via tagged Docker Images.
- Runbooks für Incidents (Checkliste).

## 10. Performance Tuning
- Warmup Cache, Multiprocessing (uvicorn workers), HTTP Keep-Alive.
- Wenn Self-host LLM: vLLM mit Tensor Parallel, kv-cache on GPU.
- CDN für Assets, Compression an.

## 11. Compliance & Policy (light)
- Datenaufbewahrung: Logs max X Tage.
- Consent Banner, Privacy Notice.
- Rechtliche Hinweise bei Gesundheits/Finanz-Themen.
