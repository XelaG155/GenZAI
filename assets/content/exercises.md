# Übungspaket – GenZAI

Dieses Paket enthält detaillierte Aufgaben, Beispiel-Lösungen, Bewertungskriterien und vorgeschlagene Tech-Stacks. Fokus: schnell iterieren, messen, shippen.

## 1. Prompting & Reasoning
- **Aufgabe:** Schreibe für ein Campus-Q&A einen System-Prompt in drei Varianten (freundlich, sachlich, knappe Antworten). Füge 3 Few-Shot-Beispiele hinzu und definiere ein Guardrail für PII.
- **Lösungsidee:** Nutze Rollenbeschreibung + Format-Check; verwende Temperatur 0.3/0.6/0.8. Baue einen PII-Filter, der Namen/Adressen maskiert.
- **Bewertung:** Konsistenz der Tonalität; Halluzinations-Quote <5%; PII wird geblockt.

## 2. RAG Basics
- **Aufgabe:** Erstelle einen Mini-RAG auf 10 PDFs (Lecture Notes). Antworte nur mit Quellen. Fallback: "Keine Quelle gefunden".
- **Lösungsidee:** Chroma + OpenAI Embeddings; Score-Threshold 0.2; Antwort mit Zitat + Link.
- **Bewertung:** Precision@5 ≥ 0.6; Quelle in 90% der Antworten; Antwortzeit < 1.8s.

## 3. RAG Hardening
- **Aufgabe:** Füge Dedup, Chunking (512 Tokens, Overlap 64) und Query-Rewriting hinzu. Logge Retrieval-Treffer.
- **Lösungsidee:** Preprocess mit LangChain/TextSplit; Query-Rewrite (LLM) → zwei Varianten; kombiniere Scores (max).
- **Bewertung:** Halluzinationsrate -30% ggü. Baseline; Top-1 Trefferquote +15%.

## 4. Vision Captioning
- **Aufgabe:** Bot akzeptiert Bild, gibt Beschreibung + TikTok-Hook. Block NSFW.
- **Lösungsidee:** Vision-Modell (GPT-4o/Llama3-Vision) + Klassifizierer (NSFW). Rate-Limit per IP.
- **Bewertung:** 0 NSFW False Negatives in 20 Bildern; Latenz < 4s; 3 Hook-Varianten.

## 5. Tool-Use Agent
- **Aufgabe:** Agent darf Wetter-API und Kalender-API nutzen. Stop nach 5 Schritten, sonst Fallback.
- **Lösungsidee:** JSON-Schema Tools; Loop-Limit; Logging jeder Action; Timeout 30s; Retry 1x.
- **Bewertung:** Erfolgsrate > 80% auf 20 Szenarien; keine Endlosschleifen; Logs enthalten Reasoning.

## 6. Eval Automation
- **Aufgabe:** Definiere 20 Testprompts (Happy/Evil/Edge). Automatisiere Score per Script.
- **Lösungsidee:** tests.yaml + Python eval; string-matching mit Regex; Latenz messen.
- **Bewertung:** CI-Check < 2m; Fail-Report mit Fehlklassifikationen.

## 7. Infra & Deploy
- **Aufgabe:** Dockerfile + docker-compose für FastAPI + Chroma + Frontend. Healthcheck bereitstellen.
- **Lösungsidee:** Multi-stage Build (Python slim); gunicorn/uvicorn; health Route `/health`; env über .env.
- **Bewertung:** `docker compose up` startet ohne Fehler; Healthcheck 200; Build < 2 min.

## 8. Security & Privacy
- **Aufgabe:** Schreibe Threat Model (STRIDE light) für dein Produkt. Baue einen Input-Filter gegen PII/NSFW.
- **Lösungsidee:** Liste Attack Vectors; Regex/ML-Filter; Key Vault nutzen; Audit-Log für Admin-Actions.
- **Bewertung:** 3 Haupt-Risiken mit Mitigation; Filter blockt 95% testbarer PII-Cases; Keys nicht im Repo.

## 9. Metrics & Analytics
- **Aufgabe:** Tracke Success Rate, Latency, Token-Kosten. Erzeuge Dashboard-Screenshot.
- **Lösungsidee:** Middleware für Timing; Kosten = tokens * price; PostHog/Sentry Events; Export als CSV.
- **Bewertung:** Dashboard zeigt 3 Metriken; 7-Tage-Trend; Alert bei Latency > 4s.

## 10. Business Case
- **Aufgabe:** Rechne Unit Economics für 3 Pläne (Free/Pro/Team). Simuliere 1k Nutzer/Monat.
- **Lösungsidee:** Excel/Notebook mit Annahmen (ARPU, Churn, Support). Szenarien Low/Base/High.
- **Bewertung:** Break-Even Monat ausgewiesen; Margen pro Plan; Sensitivität dargestellt.

---
## Abgaberegeln
- Code + README + kurze Loom/MP4 Demo (90s).
- Messbare KPIs angeben (Latency, Success, Kosten).
- Git Commit pro Übung; Tag Releases: v0.1, v0.2 …
