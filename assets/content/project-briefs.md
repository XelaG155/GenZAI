# Projekt-Briefs – von 0 auf Launch

Nutze diese Briefs als vollständige Blaupausen. Jede enthält Zielgruppe, Pain, USP, Architektur, Roadmap und KPI-Set.

## Brief A: Campus Copilot
- **Zielgruppe:** Studierende, Tutor:innen.
- **Pain:** Lange Skripte, keine schnelle Antwort, wenig Kontext.
- **USP:** Quellenbasierte Antworten + Audio-Zusammenfassungen.
- **Architektur:** FastAPI, Chroma, GPT-4o, Whisper; Frontend: Next.js.
- **Roadmap:**
  - Woche 1: Problem-Interviews, Datensammlung, Prompt v1
  - Woche 2: RAG MVP, Logging, Eval-Suite (20 Fragen)
  - Woche 3: UI Polish, Audio-Ausgabe, Rate-Limits
  - Woche 4: Launch an Fachschaften, Semester-Pass Pricing
- **KPIs:** Precision@5, Quelle-Quote, Antwortzeit, Aktivierungen/Tag.

## Brief B: Creator Content Lab
- **Zielgruppe:** Video-Creators (TikTok, Reels, YT Shorts).
- **Pain:** Ideen-Flaute, Schreibblockade, Thumbnail-Design.
- **USP:** Hook-Generator + Shotlist + Thumbnail-Sketch in 1 Minute.
- **Architektur:** Next.js, OpenAI API, Replicate SDXL; optional Notion Sync.
- **Roadmap:**
  - Woche 1: Hook-Formate sammeln, Prompt-Template
  - Woche 2: Skript + Shotlist Generator, Telemetry
  - Woche 3: Thumbnail Generation, A/B Hooks, Export CSV
  - Woche 4: Launch Stream + Referral Codes
- **KPIs:** CTR auf Hooks, Generierungszeit, Wiederkehrende Creator.

## Brief C: Local Biz Ops
- **Zielgruppe:** Kleine Shops, Cafés, Studios.
- **Pain:** Antworten auf Anfragen, Reviews, Termine frisst Zeit.
- **USP:** AI-Sekretariat mit Review-Reply, FAQ, Termin-Link.
- **Architektur:** Twilio/WhatsApp, GPT-4o mini, Supabase, optional TTS.
- **Roadmap:**
  - Woche 1: FAQ sammeln, Tonalität definieren
  - Woche 2: Chatbot + Review-Responder, Logs
  - Woche 3: Analytics Dashboard, Guardrails, Rate-Limits
  - Woche 4: Beta mit 5 Shops, Pricing Pro/Team
- **KPIs:** First Response Time, Automationsrate, Zufriedenheit.

## Brief D: Eco Impact Radar
- **Zielgruppe:** Conscious Shopper, Nachhaltigkeits-Blogs.
- **Pain:** Keine Klarheit über CO₂/Alternativen.
- **USP:** Scans Produkte, bewertet Impact, liefert Alternativen.
- **Architektur:** Browserless Scraper, LLM Judge, Supabase, optional Chrome Ext.
- **Roadmap:**
  - Woche 1: Datenquellen, Metriken, Prompt für Bewertung
  - Woche 2: Scraper + Extractor, LLM-Ranker
  - Woche 3: UI Cards, Caching, Rate-Limit, Logging
  - Woche 4: Launch mit Affiliate Links, Newsletter
- **KPIs:** Coverage, Antwortzeit, Conversion auf Affiliate Links.

## Brief E: Event Buddy
- **Zielgruppe:** Student Clubs, Party Hosts.
- **Pain:** Planung, Checklisten, Promo dauert.
- **USP:** Budget + Playlist + Einkauf + Promo-Posts in einem Flow.
- **Architektur:** Llama3 via Ollama, Edge Functions (Vercel), Supabase.
- **Roadmap:**
  - Woche 1: Personas + Anforderungen
  - Woche 2: Prompt Flows für Budget/Playlist/Promo
  - Woche 3: Automatisierte Checklisten, Payment-Links
  - Woche 4: Launch mit Insta-Takeover + Templates
- **KPIs:** Zeitersparnis, Anzahl geplanter Events, User-NPS.

## Brief F: Health & Wellness (Non-diagnostic)
- **Zielgruppe:** Fitness/Wellness Enthusiasts.
- **Pain:** Unklare Pläne, Motivation, falsche Infos.
- **USP:** Tagesplan + Einkauf + Motivationstext, kein Medical Advice.
- **Architektur:** Policy-gesichertes LLM, Content Filter, CMS für Pläne.
- **Roadmap:**
  - Woche 1: Legal/Compliance Check, Safe Prompt
  - Woche 2: Content Library + Retrieval
  - Woche 3: UX für Pläne + Push Notifications
  - Woche 4: Soft Launch mit Feedback-Loop
- **KPIs:** Engagement/Tag, Plan Completion, Safety-Flags.
