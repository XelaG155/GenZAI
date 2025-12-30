# Infrastruktur Playbook - GenZAI

Alles was du brauchst um von "läuft auf meinem Laptop" zu "läuft im Internet" zu kommen.

---

## Kapitel 1: Grundlagen

### Was ist ein Server?

Ein Server ist ein Computer der 24/7 läuft und über das Internet erreichbar ist. Statt einen echten Computer zu kaufen, mietest du eine **Virtual Machine (VM)** in einem Rechenzentrum.

```
Dein Laptop          →    VM in der Cloud
- Läuft wenn du willst    - Läuft immer
- Nur du erreichst es     - Jeder kann es erreichen
- Dein WLAN               - Datacenter Internet
```

### VM Optionen

| Typ | Wofür? | Kosten |
|-----|--------|--------|
| **CPU VM** | Websites, APIs, RAG | 5-50€/mo |
| **GPU VM** | Eigene Modelle hosten | 50-500€/mo |
| **Serverless** | Kleine Functions | 0-20€/mo |

**Für 99% der AI-Projekte reicht eine CPU VM!** Du nutzt ja APIs (OpenAI, etc.) – die haben die GPUs.

### Provider Empfehlungen

**Budget (5-20€):**
- **Hetzner** - Deutsch, günstig, solide
- **Scaleway** - EU, gute Free Tier
- **Contabo** - Sehr günstig, okay Performance

**Easy Start (10-50€):**
- **DigitalOcean** - Super Docs, simple UI
- **Render** - Git-Push = Deploy
- **Railway** - Für Entwickler gemacht

**Enterprise:**
- **AWS** - Alles möglich, komplex
- **GCP** - Google Cloud
- **Azure** - Microsoft

### Meine Empfehlung

```
Erstes Projekt? → Render oder Railway (am einfachsten)
Budget knapp?   → Hetzner Cloud
Mehr Kontrolle? → DigitalOcean
```

---

## Kapitel 2: Server Setup (Hetzner Beispiel)

### Schritt 1: Account & VM erstellen

1. Gehe zu [hetzner.cloud](https://hetzner.cloud)
2. Account erstellen
3. Neues Projekt anlegen
4. Server hinzufügen:
   - **Location:** Nürnberg oder Falkenstein
   - **Image:** Ubuntu 22.04
   - **Type:** CX21 (2 vCPU, 4GB RAM) - ~5€/mo
   - **SSH Key:** Füge deinen Public Key hinzu

### Schritt 2: SSH Key erstellen (falls nicht vorhanden)

```bash
# Auf deinem Laptop
ssh-keygen -t ed25519 -C "deine@email.com"

# Enter drücken für default Speicherort
# Passwort optional

# Public Key anzeigen (das kommt zu Hetzner)
cat ~/.ssh/id_ed25519.pub
```

### Schritt 3: Verbinden

```bash
# IP Adresse von Hetzner Dashboard
ssh root@YOUR_SERVER_IP

# Wenn es klappt siehst du:
# root@ubuntu-server:~#
```

### Schritt 4: Basis-Setup

```bash
# System updaten
apt update && apt upgrade -y

# Wichtige Tools installieren
apt install -y git curl wget htop ufw

# Neuen User anlegen (nicht als root arbeiten!)
adduser deploy
usermod -aG sudo deploy

# SSH für neuen User einrichten
mkdir -p /home/deploy/.ssh
cp ~/.ssh/authorized_keys /home/deploy/.ssh/
chown -R deploy:deploy /home/deploy/.ssh

# Testen: Neues Terminal öffnen
ssh deploy@YOUR_SERVER_IP
```

### Schritt 5: Firewall

```bash
# Nur diese Ports erlauben
sudo ufw allow 22    # SSH
sudo ufw allow 80    # HTTP
sudo ufw allow 443   # HTTPS

# Firewall aktivieren
sudo ufw enable

# Status checken
sudo ufw status
```

### Schritt 6: SSH absichern

```bash
sudo nano /etc/ssh/sshd_config

# Diese Zeilen ändern/hinzufügen:
PermitRootLogin no
PasswordAuthentication no
PubkeyAuthentication yes

# SSH neu starten
sudo systemctl restart sshd

# WICHTIG: Teste in neuem Terminal ob Login noch geht!
```

---

## Kapitel 3: Docker

### Was ist Docker?

Docker "verpackt" deine App + alle Dependencies in einen Container. Das garantiert: Was auf deinem Laptop läuft, läuft auch auf dem Server.

```
Ohne Docker:
- "Bei mir geht's"
- Auf Server: Falsche Python Version, fehlende Libs
- 3 Stunden Debugging

Mit Docker:
- Container enthält ALLES
- Läuft überall gleich
- 5 Minuten Deploy
```

### Docker installieren

```bash
# Auf dem Server
curl -fsSL https://get.docker.com | sh

# User zur Docker-Gruppe hinzufügen
sudo usermod -aG docker $USER

# WICHTIG: Ausloggen und neu einloggen

# Testen
docker run hello-world
```

### Dockerfile schreiben

```dockerfile
# Dockerfile für eine Python FastAPI App

# Basis-Image
FROM python:3.11-slim

# Arbeitsverzeichnis im Container
WORKDIR /app

# Dependencies zuerst kopieren (für besseres Caching)
COPY requirements.txt .

# Dependencies installieren
RUN pip install --no-cache-dir -r requirements.txt

# Rest der App kopieren
COPY . .

# Port freigeben
EXPOSE 8000

# Healthcheck
HEALTHCHECK --interval=30s --timeout=3s \
  CMD curl -f http://localhost:8000/health || exit 1

# Start-Befehl
CMD ["uvicorn", "main:app", "--host", "0.0.0.0", "--port", "8000"]
```

### Docker Compose

Für Apps mit mehreren Services (z.B. API + Datenbank):

```yaml
# docker-compose.yml
version: '3.8'

services:
  api:
    build: .
    ports:
      - "8000:8000"
    env_file:
      - .env
    depends_on:
      - chroma
    restart: unless-stopped
    healthcheck:
      test: ["CMD", "curl", "-f", "http://localhost:8000/health"]
      interval: 30s
      timeout: 10s
      retries: 3

  chroma:
    image: chromadb/chroma:latest
    ports:
      - "8001:8000"
    volumes:
      - chroma_data:/chroma/chroma
    environment:
      - IS_PERSISTENT=TRUE
    restart: unless-stopped

volumes:
  chroma_data:
```

### Docker Befehle

```bash
# Image bauen
docker compose build

# Container starten
docker compose up -d

# Logs anschauen
docker compose logs -f
docker compose logs api  # Nur ein Service

# Status
docker compose ps

# Stoppen
docker compose down

# Neustarten nach Code-Änderung
docker compose build && docker compose up -d
```

---

## Kapitel 4: Deployment

### Option A: Manuelles Deploy

```bash
# Auf dem Server

# 1. Repo clonen (einmalig)
git clone https://github.com/YOUR_USER/YOUR_REPO.git
cd YOUR_REPO

# 2. .env Datei erstellen
nano .env
# OPENAI_API_KEY=sk-...
# Speichern mit Ctrl+X, dann Y, dann Enter

# 3. Starten
docker compose up -d

# 4. Bei Updates
git pull
docker compose build
docker compose up -d
```

### Option B: GitHub Actions (Automatisch)

```yaml
# .github/workflows/deploy.yml
name: Deploy

on:
  push:
    branches: [main]

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - name: Deploy to Server
        uses: appleboy/ssh-action@v1.0.0
        with:
          host: ${{ secrets.SERVER_IP }}
          username: deploy
          key: ${{ secrets.SSH_PRIVATE_KEY }}
          script: |
            cd ~/YOUR_REPO
            git pull origin main
            docker compose build
            docker compose up -d
```

**GitHub Secrets einrichten:**
1. Repo → Settings → Secrets and variables → Actions
2. `SERVER_IP`: Deine Server IP
3. `SSH_PRIVATE_KEY`: Inhalt von `~/.ssh/id_ed25519`

---

## Kapitel 5: HTTPS & Domain

### Domain kaufen

Günstige Optionen:
- **Namecheap** - Ab ~10€/Jahr
- **Cloudflare** - Zum Einkaufspreis
- **Porkbun** - Günstig + gute UI

### DNS einrichten

In deinem Domain-Dashboard:
```
Type: A
Name: @ (oder subdomain)
Value: YOUR_SERVER_IP
TTL: 300
```

### Caddy (Easy HTTPS)

Caddy ist ein Webserver der HTTPS automatisch einrichtet:

```bash
# Caddy installieren
sudo apt install -y debian-keyring debian-archive-keyring apt-transport-https
curl -1sLf 'https://dl.cloudsmith.io/public/caddy/stable/gpg.key' | sudo gpg --dearmor -o /usr/share/keyrings/caddy-stable-archive-keyring.gpg
curl -1sLf 'https://dl.cloudsmith.io/public/caddy/stable/debian.deb.txt' | sudo tee /etc/apt/sources.list.d/caddy-stable.list
sudo apt update
sudo apt install caddy

# Caddyfile erstellen
sudo nano /etc/caddy/Caddyfile
```

```
# /etc/caddy/Caddyfile
yourdomain.com {
    reverse_proxy localhost:8000
}

# Für Subdomains
api.yourdomain.com {
    reverse_proxy localhost:8000
}
```

```bash
# Caddy neu starten
sudo systemctl restart caddy

# Status checken
sudo systemctl status caddy

# Logs
sudo journalctl -u caddy -f
```

**Das war's!** Caddy holt automatisch ein SSL-Zertifikat von Let's Encrypt.

---

## Kapitel 6: Monitoring

### Basic: Docker Logs

```bash
# Alle Logs
docker compose logs -f

# Nur Errors
docker compose logs -f 2>&1 | grep -i error

# Letzte 100 Zeilen
docker compose logs --tail 100
```

### Health Checks

```python
# main.py - FastAPI Health Endpoint
from fastapi import FastAPI

app = FastAPI()

@app.get("/health")
def health():
    return {"status": "healthy"}

@app.get("/ready")
def ready():
    # Check database connection etc.
    return {"status": "ready"}
```

### Uptime Monitoring

Kostenlose Optionen:
- **UptimeRobot** - 50 Monitore gratis
- **Healthchecks.io** - Für Cronjobs
- **Better Uptime** - Schöne UI

Einrichten:
1. Account erstellen
2. Monitor hinzufügen: `https://yourdomain.com/health`
3. Alert: Email oder Slack

### Metriken loggen

```python
import time
import logging

logging.basicConfig(level=logging.INFO)
logger = logging.getLogger(__name__)

@app.middleware("http")
async def log_requests(request, call_next):
    start = time.time()
    response = await call_next(request)
    duration = time.time() - start

    logger.info(
        f"{request.method} {request.url.path} "
        f"status={response.status_code} "
        f"duration={duration:.3f}s"
    )
    return response
```

---

## Kapitel 7: Kosten

### Beispiel-Kalkulation

```
MVP / Side Project:
- Hetzner CX21:        4.51€/mo
- Domain:              ~1€/mo
- OpenAI API:          ~10-20€/mo
                       ──────────
Total:                 ~20€/mo

Mit zahlenden Usern:
- Hetzner CX31:        8.21€/mo
- Domain:              ~1€/mo
- OpenAI API:          ~50€/mo
- Monitoring:          0€ (Free Tier)
                       ──────────
Total:                 ~60€/mo
```

### Kosten senken

1. **Richtige VM-Größe**: Starte klein, skaliere bei Bedarf
2. **Caching**: Häufige Anfragen cachen
3. **Günstigere Modelle**: gpt-4o-mini statt gpt-4
4. **Rate Limits**: Abuse verhindern
5. **Auto-Shutdown**: Dev-Server nachts ausschalten

### API Kosten tracken

```python
# Token Tracking
import tiktoken

def count_tokens(text: str, model: str = "gpt-4o-mini") -> int:
    encoding = tiktoken.encoding_for_model(model)
    return len(encoding.encode(text))

# In deinem API Call
def log_usage(prompt: str, response: str, model: str):
    input_tokens = count_tokens(prompt, model)
    output_tokens = count_tokens(response, model)

    # GPT-4o-mini Preise (Stand 2024)
    input_cost = input_tokens * 0.00000015
    output_cost = output_tokens * 0.0000006

    logger.info(
        f"Tokens: {input_tokens} in, {output_tokens} out | "
        f"Cost: ${input_cost + output_cost:.6f}"
    )
```

---

## Kapitel 8: Security Checklist

### Vor dem Launch

- [ ] SSH nur mit Key-Auth (kein Passwort)
- [ ] Firewall aktiv (nur 22, 80, 443)
- [ ] Root-Login deaktiviert
- [ ] System Updates installiert
- [ ] Docker Images aktuell

### Für die App

- [ ] .env nicht im Git
- [ ] API Keys im Secret Manager oder .env
- [ ] HTTPS überall
- [ ] Rate Limiting aktiv
- [ ] Input Validation
- [ ] CORS korrekt konfiguriert

### Regelmäßig

- [ ] Weekly: Logs auf Anomalien prüfen
- [ ] Monthly: System Updates
- [ ] Quarterly: Dependencies updaten

---

## Kapitel 9: Troubleshooting

### Container startet nicht

```bash
# Logs prüfen
docker compose logs api

# Häufige Fehler:
# - Port bereits belegt
# - .env Datei fehlt
# - Dependency Error
```

### App nicht erreichbar

```bash
# 1. Container läuft?
docker compose ps

# 2. Port offen?
sudo ufw status

# 3. Caddy läuft?
sudo systemctl status caddy

# 4. Caddy Logs
sudo journalctl -u caddy -f

# 5. Kann der Server sich selbst erreichen?
curl localhost:8000/health
```

### Speicher voll

```bash
# Speicher prüfen
df -h

# Docker aufräumen
docker system prune -a

# Alte Logs löschen
sudo journalctl --vacuum-size=100M
```

### Server langsam

```bash
# CPU/RAM prüfen
htop

# Welcher Container frisst Ressourcen?
docker stats

# Lösung: Größere VM oder App optimieren
```

---

## Quick Reference

### Wichtige Befehle

```bash
# SSH
ssh deploy@YOUR_IP

# Docker
docker compose up -d        # Starten
docker compose down         # Stoppen
docker compose logs -f      # Logs
docker compose ps           # Status
docker compose build        # Neu bauen

# System
htop                        # Ressourcen
df -h                       # Speicher
sudo ufw status            # Firewall

# Caddy
sudo systemctl restart caddy
sudo journalctl -u caddy -f

# Updates
sudo apt update && sudo apt upgrade -y
```

### Wichtige Dateien

```
/home/deploy/YOUR_REPO/
├── .env                    # Secrets
├── docker-compose.yml      # Container Config
├── Dockerfile              # Build Config
└── ...

/etc/caddy/Caddyfile        # HTTPS Config
/var/log/                   # System Logs
```

### Notfall-Kontakte

- Hetzner Support: [docs.hetzner.com](https://docs.hetzner.com)
- Docker Docs: [docs.docker.com](https://docs.docker.com)
- Caddy Docs: [caddyserver.com/docs](https://caddyserver.com/docs)

---

## Next Steps

1. **Erstes Deploy**: Folge Kapitel 2-5 Schritt für Schritt
2. **Monitoring**: Richte UptimeRobot ein
3. **Automatisierung**: GitHub Actions für Auto-Deploy
4. **Skalierung**: Bei Bedarf größere VM oder mehrere Container

Du hast das. Ship it! 🚀
