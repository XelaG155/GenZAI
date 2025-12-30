# Übungen & Labs - GenZAI

Hands-on Aufgaben mit Lösungen. Jede Übung hat klare Ziele, Tech-Stack und Bewertungskriterien.

---

## Modul 1: Foundations

### Übung 1.1: Prompt Engineering Battle

**Ziel:** Verstehe, wie unterschiedliche Prompts zu unterschiedlichen Outputs führen.

**Aufgabe:**
1. Nimm diesen Basic-Prompt: "Erkläre mir Machine Learning"
2. Erstelle 3 Varianten:
   - **Version A:** Für einen 10-Jährigen
   - **Version B:** Für einen Informatik-Studenten
   - **Version C:** Als TikTok-Script (max 60 Sekunden)
3. Teste alle 3 mit GPT-4 oder Claude
4. Dokumentiere die Unterschiede

**Lösung:**
```
Version A - System Prompt:
"Du erklärst Konzepte wie ein freundlicher Lehrer für Grundschüler.
Nutze einfache Wörter, Analogien aus dem Alltag und kurze Sätze."

Version B - System Prompt:
"Du bist ein Informatik-Tutor. Erkläre präzise mit Fachbegriffen,
erwähne relevante Algorithmen und mathematische Grundlagen."

Version C - System Prompt:
"Du schreibst virale TikTok Scripts. Hook in den ersten 2 Sekunden,
dann schnelle Erklärung, Ende mit Call-to-Action. Max 150 Wörter."
```

**Bewertung:**
- [ ] Alle 3 Versionen haben unterschiedlichen Ton
- [ ] Version A verwendet keine Fachbegriffe
- [ ] Version B ist technisch korrekt
- [ ] Version C hat Hook + CTA

---

### Übung 1.2: Halluzinations-Detektor

**Ziel:** Lerne, Halluzinationen zu erkennen und zu vermeiden.

**Aufgabe:**
1. Stelle der AI 10 Fragen zu einem Nischen-Thema (z.B. deine Uni, lokale Events)
2. Prüfe jede Antwort auf Fakten
3. Zähle die Halluzinationen
4. Schreibe einen Prompt, der Halluzinationen reduziert

**Lösung:**
```python
# Anti-Halluzinations Prompt Template
system_prompt = """
Du bist ein faktenbasierter Assistent. Befolge diese Regeln strikt:

1. Wenn du etwas nicht sicher weißt, sage "Ich bin mir nicht sicher" oder "Das müsste ich nachprüfen"
2. Unterscheide klar zwischen Fakten und Vermutungen
3. Gib keine spezifischen Zahlen, Daten oder Namen an, wenn du dir nicht 100% sicher bist
4. Bei Unsicherheit: Lieber zu wenig als zu viel behaupten

Beginne deine Antwort IMMER mit einer Einschätzung deiner Konfidenz:
- 🟢 Hohe Sicherheit: Das ist gut dokumentiertes Wissen
- 🟡 Mittlere Sicherheit: Könnte veraltet oder unvollständig sein
- 🔴 Niedrige Sicherheit: Besser selbst nachprüfen
"""
```

**Bewertung:**
- [ ] Mindestens 3 Halluzinationen gefunden
- [ ] Anti-Halluzinations-Prompt reduziert Fehler um >50%
- [ ] Dokumentation der gefundenen Fehler

---

### Übung 1.3: Few-Shot Learning

**Ziel:** Nutze Beispiele statt Erklärungen.

**Aufgabe:**
Erstelle einen Prompt, der Produktbeschreibungen in Marketing-Copy umwandelt.

**Input-Beispiel:**
"Bluetooth Kopfhörer, 40h Akku, Active Noise Cancelling, faltbar"

**Gewünschter Output:**
"Tschüss Lärm, Hallo Musik. 40 Stunden pure Freiheit - faltbar für überall."

**Lösung:**
```
Du wandelst trockene Produktbeschreibungen in catchy Marketing-Copy um.

Beispiele:

Input: "Rucksack, 30L, wasserdicht, Laptopfach bis 15 Zoll"
Output: "Dein Office für unterwegs. Wasserdicht wenn's schüttet, Platz für alles was zählt."

Input: "Sneaker, Memory Foam Sohle, atmungsaktiv, 6 Farben"
Output: "Läuft wie auf Wolken. Deine Füße werden's dir danken - in deiner Lieblingsfarbe."

Input: "Smartwatch, Herzfrequenz, GPS, 7 Tage Akku"
Output: "Dein Körper in Zahlen. Eine Woche Power am Handgelenk."

Jetzt du:
Input: "{{PRODUKT_BESCHREIBUNG}}"
Output:
```

**Bewertung:**
- [ ] 3-5 Beispiele im Prompt
- [ ] Konsistenter Stil über alle Outputs
- [ ] Outputs sind kürzer als Inputs

---

## Modul 2: Build Lab

### Übung 2.1: Erster API Call

**Ziel:** Mache deinen ersten erfolgreichen API Call.

**Aufgabe:**
1. Erstelle einen OpenAI Account (falls nicht vorhanden)
2. Generiere einen API Key
3. Schreibe ein Python Script, das eine Frage beantwortet
4. Logge Token-Verbrauch und Kosten

**Lösung:**
```python
import os
from openai import OpenAI
from dotenv import load_dotenv

load_dotenv()

client = OpenAI()

def ask_ai(question: str) -> dict:
    response = client.chat.completions.create(
        model="gpt-4o-mini",
        messages=[
            {"role": "system", "content": "Du bist ein hilfreicher Assistent."},
            {"role": "user", "content": question}
        ]
    )

    # Token Tracking
    usage = response.usage

    # Kosten berechnen (gpt-4o-mini Preise)
    input_cost = usage.prompt_tokens * 0.00000015
    output_cost = usage.completion_tokens * 0.0000006
    total_cost = input_cost + output_cost

    return {
        "answer": response.choices[0].message.content,
        "input_tokens": usage.prompt_tokens,
        "output_tokens": usage.completion_tokens,
        "cost_usd": round(total_cost, 6)
    }

# Test
result = ask_ai("Was ist der Unterschied zwischen RAG und Fine-tuning?")
print(f"Antwort: {result['answer']}")
print(f"Tokens: {result['input_tokens']} in, {result['output_tokens']} out")
print(f"Kosten: ${result['cost_usd']}")
```

**Bewertung:**
- [ ] API Key sicher in .env gespeichert
- [ ] Script läuft ohne Fehler
- [ ] Token-Tracking funktioniert
- [ ] Kosten werden korrekt berechnet

---

### Übung 2.2: Mini-RAG System

**Ziel:** Baue ein funktionierendes RAG mit 5 Dokumenten.

**Aufgabe:**
1. Sammle 5 PDF-Dokumente (z.B. Uni-Skripte, Anleitungen)
2. Extrahiere den Text und erstelle Chunks
3. Speichere in ChromaDB
4. Baue eine Abfrage-Funktion mit Quellenangabe

**Lösung:**
```python
import chromadb
from chromadb.utils import embedding_functions
from langchain.document_loaders import PyPDFLoader
from langchain.text_splitter import RecursiveCharacterTextSplitter
import os

# Setup
openai_ef = embedding_functions.OpenAIEmbeddingFunction(
    api_key=os.getenv("OPENAI_API_KEY"),
    model_name="text-embedding-3-small"
)

client = chromadb.Client()
collection = client.create_collection(
    name="my_docs",
    embedding_function=openai_ef
)

# Dokumente laden
def load_pdfs(folder_path: str):
    documents = []
    for filename in os.listdir(folder_path):
        if filename.endswith(".pdf"):
            loader = PyPDFLoader(os.path.join(folder_path, filename))
            pages = loader.load()
            for page in pages:
                page.metadata["source"] = filename
            documents.extend(pages)
    return documents

# Chunking
splitter = RecursiveCharacterTextSplitter(
    chunk_size=500,
    chunk_overlap=50,
    separators=["\n\n", "\n", ". ", " ", ""]
)

docs = load_pdfs("./documents")
chunks = splitter.split_documents(docs)

# In Chroma speichern
for i, chunk in enumerate(chunks):
    collection.add(
        documents=[chunk.page_content],
        metadatas=[{
            "source": chunk.metadata.get("source", "unknown"),
            "page": chunk.metadata.get("page", 0)
        }],
        ids=[f"chunk_{i}"]
    )

print(f"✅ {len(chunks)} Chunks gespeichert")

# Abfrage mit Quellen
def query_with_sources(question: str, n_results: int = 3):
    results = collection.query(
        query_texts=[question],
        n_results=n_results
    )

    contexts = []
    for doc, meta, distance in zip(
        results["documents"][0],
        results["metadatas"][0],
        results["distances"][0]
    ):
        contexts.append({
            "text": doc,
            "source": meta["source"],
            "page": meta["page"],
            "score": 1 - distance  # Convert distance to similarity
        })

    return contexts

# Test
results = query_with_sources("Was ist Machine Learning?")
for r in results:
    print(f"[{r['source']}, S.{r['page']}] Score: {r['score']:.2f}")
    print(f"  {r['text'][:100]}...")
```

**Bewertung:**
- [ ] Mindestens 5 PDFs verarbeitet
- [ ] Chunks sind sinnvoll (nicht mitten im Satz)
- [ ] Abfrage liefert relevante Ergebnisse
- [ ] Quellenangabe funktioniert

---

### Übung 2.3: RAG mit Guardrails

**Ziel:** Baue Sicherheitsmechanismen ein.

**Aufgabe:**
Erweitere dein RAG um:
1. Score-Threshold (nur antworten wenn Score > 0.3)
2. Fallback-Nachricht bei schlechten Ergebnissen
3. PII-Filter für Input

**Lösung:**
```python
import re
from openai import OpenAI

client = OpenAI()

def filter_pii(text: str) -> str:
    """Entfernt potenzielle PII aus dem Input"""
    # Email
    text = re.sub(r'\b[\w.-]+@[\w.-]+\.\w+\b', '[EMAIL]', text)
    # Telefon (deutsch)
    text = re.sub(r'\b(\+49|0)[0-9\s\-/]{8,15}\b', '[TELEFON]', text)
    # IBAN
    text = re.sub(r'\b[A-Z]{2}\d{2}[A-Z0-9]{4,30}\b', '[IBAN]', text)
    return text

def rag_with_guardrails(question: str, min_score: float = 0.3):
    # PII Filter
    clean_question = filter_pii(question)

    # Retrieve
    results = query_with_sources(clean_question, n_results=3)

    # Score Check
    if not results or results[0]["score"] < min_score:
        return {
            "answer": "Ich habe leider keine passende Information in den Dokumenten gefunden. Kannst du deine Frage anders formulieren?",
            "sources": [],
            "confidence": "low"
        }

    # Context zusammenbauen
    context = "\n\n".join([
        f"[Quelle: {r['source']}, S.{r['page']}]\n{r['text']}"
        for r in results if r["score"] >= min_score
    ])

    # Generate
    response = client.chat.completions.create(
        model="gpt-4o-mini",
        messages=[
            {
                "role": "system",
                "content": """Du beantwortest Fragen basierend auf dem gegebenen Kontext.

Regeln:
- Antworte NUR basierend auf dem Kontext
- Wenn der Kontext die Frage nicht beantwortet, sage das ehrlich
- Gib immer die Quelle an (Dokument + Seite)
- Keine Spekulationen oder Zusatzinfos"""
            },
            {
                "role": "user",
                "content": f"Kontext:\n{context}\n\nFrage: {clean_question}"
            }
        ]
    )

    return {
        "answer": response.choices[0].message.content,
        "sources": [{"source": r["source"], "page": r["page"]} for r in results],
        "confidence": "high" if results[0]["score"] > 0.5 else "medium"
    }
```

**Bewertung:**
- [ ] PII wird gefiltert (teste mit Email/Telefon)
- [ ] Niedrige Scores triggern Fallback
- [ ] Quellenangabe in der Antwort
- [ ] Keine Halluzinationen bei "off-topic" Fragen

---

## Modul 3: Infrastruktur

### Übung 3.1: Docker Basics

**Ziel:** Containerisiere deine App.

**Aufgabe:**
1. Schreibe ein Dockerfile für eine FastAPI App
2. Erstelle docker-compose.yml mit API + Chroma
3. Baue und starte den Container
4. Teste mit curl

**Lösung:**
```dockerfile
# Dockerfile
FROM python:3.11-slim

# Arbeitsverzeichnis
WORKDIR /app

# Dependencies zuerst (für besseres Caching)
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

# App Code
COPY . .

# Port
EXPOSE 8000

# Healthcheck
HEALTHCHECK --interval=30s --timeout=3s \
  CMD curl -f http://localhost:8000/health || exit 1

# Start
CMD ["uvicorn", "main:app", "--host", "0.0.0.0", "--port", "8000"]
```

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

  chroma:
    image: chromadb/chroma:latest
    ports:
      - "8001:8000"
    volumes:
      - chroma_data:/chroma/chroma
    environment:
      - IS_PERSISTENT=TRUE

volumes:
  chroma_data:
```

```bash
# Befehle zum Testen
docker compose build
docker compose up -d
curl http://localhost:8000/health
docker compose logs -f api
```

**Bewertung:**
- [ ] Container baut ohne Fehler
- [ ] App startet und ist erreichbar
- [ ] Healthcheck funktioniert
- [ ] Daten persistieren nach Restart

---

### Übung 3.2: Server Setup

**Ziel:** Deploye auf einem echten Server.

**Aufgabe:**
1. Miete eine VM (Hetzner, DigitalOcean, etc.)
2. Installiere Docker
3. Deploye deine App
4. Richte HTTPS ein

**Checkliste:**
```bash
# 1. SSH Verbindung
ssh root@YOUR_IP

# 2. System Update
sudo apt update && sudo apt upgrade -y

# 3. Docker installieren
curl -fsSL https://get.docker.com | sh
sudo usermod -aG docker $USER
# Ausloggen, neu einloggen

# 4. Repo clonen
git clone https://github.com/YOUR_USER/YOUR_REPO.git
cd YOUR_REPO

# 5. App starten
docker compose up -d

# 6. Caddy für HTTPS
sudo apt install caddy
sudo nano /etc/caddy/Caddyfile
# Inhalt:
# yourdomain.com {
#     reverse_proxy localhost:8000
# }
sudo systemctl restart caddy

# 7. Firewall
sudo ufw allow 22
sudo ufw allow 80
sudo ufw allow 443
sudo ufw enable
```

**Bewertung:**
- [ ] App ist über Domain erreichbar
- [ ] HTTPS funktioniert (grünes Schloss)
- [ ] Firewall ist aktiv
- [ ] SSH Key-Auth only (kein Passwort)

---

## Modul 4: AI Patterns

### Übung 4.1: Function Calling

**Ziel:** Baue einen Agent mit Tools.

**Aufgabe:**
Erstelle einen Assistenten, der:
1. Wetter abfragen kann
2. Termine erstellen kann
3. Notizen speichern kann

**Lösung:**
```python
from openai import OpenAI
import json

client = OpenAI()

# Tool Definitionen
tools = [
    {
        "type": "function",
        "function": {
            "name": "get_weather",
            "description": "Holt aktuelle Wetterdaten für eine Stadt",
            "parameters": {
                "type": "object",
                "properties": {
                    "city": {
                        "type": "string",
                        "description": "Name der Stadt"
                    }
                },
                "required": ["city"]
            }
        }
    },
    {
        "type": "function",
        "function": {
            "name": "create_event",
            "description": "Erstellt einen Kalendereintrag",
            "parameters": {
                "type": "object",
                "properties": {
                    "title": {"type": "string"},
                    "date": {"type": "string", "description": "Format: YYYY-MM-DD"},
                    "time": {"type": "string", "description": "Format: HH:MM"}
                },
                "required": ["title", "date"]
            }
        }
    },
    {
        "type": "function",
        "function": {
            "name": "save_note",
            "description": "Speichert eine Notiz",
            "parameters": {
                "type": "object",
                "properties": {
                    "content": {"type": "string"},
                    "tags": {
                        "type": "array",
                        "items": {"type": "string"}
                    }
                },
                "required": ["content"]
            }
        }
    }
]

# Mock Implementierungen
def get_weather(city: str) -> str:
    return f"In {city} sind es aktuell 18°C, leicht bewölkt."

def create_event(title: str, date: str, time: str = None) -> str:
    return f"Termin '{title}' am {date} {time or ''} erstellt."

def save_note(content: str, tags: list = None) -> str:
    return f"Notiz gespeichert. Tags: {tags or []}"

# Tool Executor
def execute_tool(name: str, args: dict) -> str:
    if name == "get_weather":
        return get_weather(**args)
    elif name == "create_event":
        return create_event(**args)
    elif name == "save_note":
        return save_note(**args)
    return "Unknown tool"

# Agent Loop
def agent(user_message: str, max_steps: int = 5):
    messages = [
        {"role": "system", "content": "Du bist ein hilfreicher Assistent mit Zugriff auf Tools."},
        {"role": "user", "content": user_message}
    ]

    for step in range(max_steps):
        response = client.chat.completions.create(
            model="gpt-4o-mini",
            messages=messages,
            tools=tools
        )

        choice = response.choices[0]

        # Keine Tool Calls = fertig
        if not choice.message.tool_calls:
            return choice.message.content

        # Tool Calls ausführen
        messages.append(choice.message)

        for tool_call in choice.message.tool_calls:
            result = execute_tool(
                tool_call.function.name,
                json.loads(tool_call.function.arguments)
            )
            messages.append({
                "role": "tool",
                "tool_call_id": tool_call.id,
                "content": result
            })

    return "Max steps reached"

# Test
print(agent("Wie ist das Wetter in Berlin und erstelle einen Termin für morgen um 14 Uhr: Meeting"))
```

**Bewertung:**
- [ ] Alle 3 Tools sind definiert
- [ ] Agent ruft richtige Tools auf
- [ ] Mehrere Tool Calls in einer Anfrage möglich
- [ ] Max Steps verhindert Endlosschleife

---

## Modul 5: Business

### Übung 5.1: Unit Economics

**Ziel:** Berechne ob dein Produkt profitabel sein kann.

**Aufgabe:**
Erstelle eine Kalkulation für dein AI-Produkt mit:
- API Kosten pro User
- Infrastruktur Kosten
- Preis pro User
- Break-Even Point

**Template:**
```python
# Unit Economics Calculator

# Annahmen
avg_requests_per_user_per_month = 100
avg_input_tokens = 500
avg_output_tokens = 200

# Kosten (GPT-4o-mini Preise)
input_price_per_1k = 0.00015
output_price_per_1k = 0.0006

# Berechnung pro User
input_cost = (avg_requests_per_user_per_month * avg_input_tokens / 1000) * input_price_per_1k
output_cost = (avg_requests_per_user_per_month * avg_output_tokens / 1000) * output_price_per_1k
api_cost_per_user = input_cost + output_cost

print(f"API Kosten pro User/Monat: ${api_cost_per_user:.4f}")

# Fixkosten
server_cost = 20  # EUR/Monat
domain_cost = 1   # EUR/Monat
fixed_costs = server_cost + domain_cost

# Pricing
price_per_user = 4.99
margin_per_user = price_per_user - api_cost_per_user

print(f"Marge pro User: ${margin_per_user:.2f}")

# Break-Even
break_even_users = fixed_costs / margin_per_user
print(f"Break-Even bei {break_even_users:.0f} zahlenden Usern")

# Szenarios
for users in [10, 50, 100, 500]:
    revenue = users * price_per_user
    variable_costs = users * api_cost_per_user
    profit = revenue - variable_costs - fixed_costs
    print(f"{users} User: Revenue ${revenue:.0f}, Profit ${profit:.0f}")
```

**Bewertung:**
- [ ] Alle Kostenarten berücksichtigt
- [ ] Break-Even realistisch erreichbar
- [ ] Marge pro User > 0
- [ ] Szenarien durchgerechnet

---

### Übung 5.2: Landing Page Copy

**Ziel:** Schreibe Copy die konvertiert.

**Aufgabe:**
Erstelle für dein AI-Produkt:
1. Headline (max 10 Wörter)
2. Subheadline (max 25 Wörter)
3. 3 Bullet Points (Benefits, nicht Features)
4. CTA Button Text
5. Social Proof Element

**Beispiel-Lösung für StudyBuddy AI:**
```
HEADLINE:
Frag dein Skript – bekomm Antworten mit Seitenzahl

SUBHEADLINE:
Lade deine Uni-PDFs hoch und chatte mit ihnen.
Nie wieder 500 Seiten durchblättern auf der Suche nach einer Info.

BENEFITS:
• Spare 5+ Stunden pro Klausur – finde jede Info in Sekunden
• Lerne mit Quellenangaben – perfekt für wissenschaftliche Arbeiten
• Funktioniert mit allen deinen Skripten, Vorlesungsfolien und Papers

CTA:
Kostenlos starten →

SOCIAL PROOF:
"Hab meine Klausurvorbereitung von 3 Tagen auf einen Nachmittag reduziert"
- Lisa, BWL Studentin TU München
```

**Bewertung:**
- [ ] Headline ist klar und spezifisch
- [ ] Benefits, nicht Features
- [ ] CTA erzeugt keine Friction ("kostenlos", "starten")
- [ ] Social Proof ist glaubwürdig

---

## Bewertungsübersicht

| Übung | Schwierigkeit | Geschätzte Zeit | Kernkompetenz |
|-------|---------------|-----------------|---------------|
| 1.1 Prompt Battle | ⭐ | 30 min | Prompting |
| 1.2 Halluzinationen | ⭐ | 45 min | Safety |
| 1.3 Few-Shot | ⭐ | 30 min | Prompting |
| 2.1 API Call | ⭐ | 20 min | API Basics |
| 2.2 Mini-RAG | ⭐⭐ | 2h | RAG |
| 2.3 Guardrails | ⭐⭐ | 1h | Safety |
| 3.1 Docker | ⭐⭐ | 1h | Infra |
| 3.2 Server | ⭐⭐⭐ | 2-3h | Deployment |
| 4.1 Function Calling | ⭐⭐ | 1.5h | Agents |
| 5.1 Unit Economics | ⭐ | 30 min | Business |
| 5.2 Landing Copy | ⭐ | 30 min | Marketing |

---

## Abgabe-Format

Für jede abgeschlossene Übung:

1. **Code** in eigenem Folder im Repo
2. **README.md** mit:
   - Was hast du gebaut?
   - Welche Probleme hattest du?
   - Was hast du gelernt?
3. **Screenshots/Demo** (Loom oder MP4, max 90 Sekunden)
4. **Messbare Ergebnisse** (Latency, Kosten, Success Rate)

```
übungen/
├── 1.1-prompt-battle/
│   ├── prompts.md
│   └── ergebnisse.md
├── 2.2-mini-rag/
│   ├── main.py
│   ├── requirements.txt
│   ├── README.md
│   └── demo.mp4
└── ...
```
