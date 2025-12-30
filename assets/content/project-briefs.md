# Projekt-Briefs - GenZAI

Komplette Blaupausen für 6 AI-Projekte. Jedes Brief enthält alles was du brauchst: Problem, Lösung, Tech Stack, Roadmap und Business Model.

---

## Brief 1: StudyBuddy AI

**Tagline:** Frag dein Skript – bekomm Antworten mit Seitenzahl

### Problem
Studierende haben hunderte Seiten Skripte, Vorlesungsfolien und Papers. Vor Klausuren suchen sie verzweifelt nach spezifischen Infos. Ctrl+F reicht nicht, weil sie oft nicht wissen wonach sie suchen.

### Lösung
Ein RAG-Chatbot der alle Uni-Dokumente versteht. User lädt PDFs hoch, stellt Fragen in natürlicher Sprache, bekommt Antworten MIT Quellenangabe (Dokument + Seitenzahl).

### Zielgruppe
- Primär: Studierende (Bachelor/Master)
- Sekundär: Tutor:innen, Fachschaften
- Nische zum Starten: Ein Studiengang an einer Uni

### Tech Stack
```
Backend:
- Python 3.11 + FastAPI
- ChromaDB (Vector Store)
- OpenAI API (gpt-4o-mini + embeddings)
- PyPDF für PDF-Parsing

Frontend:
- Next.js 14
- Tailwind CSS
- Vercel Deployment

Infra:
- Hetzner VM (CX21, ~5€/Monat)
- oder Render Free Tier zum Start
```

### Features MVP
1. PDF Upload (max 5 Dokumente, max 50MB gesamt)
2. Chat Interface
3. Antworten mit Quellenangabe
4. Einfaches User Auth (Magic Link)

### Features Later
- Mehr Dokumente
- Zusammenfassungen generieren
- Karteikarten erstellen
- Team/Fachschafts-Accounts
- Audio-Zusammenfassungen

### Roadmap
```
WOCHE 1:
- [ ] 5-10 Studis befragen
- [ ] Tech Setup (Repo, Environments)
- [ ] PDF Parsing + Chunking

WOCHE 2:
- [ ] RAG Pipeline funktioniert
- [ ] Basis UI (Chat)
- [ ] 5 Testuser

WOCHE 3:
- [ ] Error Handling
- [ ] Rate Limiting
- [ ] Deploy auf Server
- [ ] Domain + HTTPS

WOCHE 4:
- [ ] Landing Page
- [ ] Auth implementieren
- [ ] Soft Launch in einer Fachschaft
```

### Pricing
| Tier | Preis | Features |
|------|-------|----------|
| Free | 0€ | 3 PDFs, 20 Fragen/Tag |
| Pro | 4.99€/mo | Unlimited |
| Student | 2.99€/mo | = Pro mit Nachweis |
| Fachschaft | 19.99€/mo | 10 Accounts, Shared Docs |

### Unit Economics
```
Kosten pro User/Monat:
- ~100 Anfragen × 700 Tokens avg = 70k Tokens
- Embedding + Generation ≈ $0.02-0.05
- Server anteilig ≈ $0.10

Marge bei 4.99€: ~4.80€ = 96%

Break-Even: ~4 zahlende User (deckt Server)
```

### Marketing
1. **Fachschafts-Partnerships**: Semester-Deals anbieten
2. **Campus Ambassadors**: 1 Student pro Uni, bekommt Pro gratis
3. **TikTok/Reels**: "POV: Du fragst dein Skript statt es zu lesen"
4. **Discord**: Study-Server joinen und helfen

### Risiken
- PDF Parsing ist tricky (Tabellen, Formeln)
- Halluzinationen bei schlechter Quellenqualität
- Rechtliche Fragen bei Urheber-geschütztem Material

---

## Brief 2: ContentForge

**Tagline:** Von Idee zu TikTok in 60 Sekunden

### Problem
Creator verbringen mehr Zeit mit Planen als mit Erstellen. Hooks schreiben, Skripte strukturieren, Hashtags recherchieren – alles dauert.

### Lösung
AI-Pipeline: Thema eingeben → Hook-Varianten → Skript → Shotlist → Hashtags. Optional: Thumbnail-Vorschläge.

### Zielgruppe
- TikTok/Reels Creator (10k-500k Follower)
- YouTube Shorts Creator
- Content Agencies

### Tech Stack
```
Backend:
- Python + FastAPI
- OpenAI API (gpt-4o)
- Optional: Replicate für Thumbnails

Frontend:
- Next.js
- Framer Motion (Animationen)

Infra:
- Vercel (Frontend)
- Railway (Backend)
```

### Features MVP
1. Hook Generator (3 Varianten)
2. Skript-Struktur (Hook → Problem → Solution → CTA)
3. Hashtag Suggestions
4. Copy-to-Clipboard überall

### Features Later
- Thumbnail AI (SDXL)
- Trending Topics Scanner
- Analytics Integration
- Team Workspaces

### Roadmap
```
WOCHE 1:
- [ ] 5 Creator befragen
- [ ] Prompt Engineering für Hooks
- [ ] Test mit 50 verschiedenen Themen

WOCHE 2:
- [ ] Full Pipeline (Hook → Skript → Hashtags)
- [ ] UI mit guter UX
- [ ] Export-Optionen

WOCHE 3:
- [ ] User Auth
- [ ] History/Favorites
- [ ] Deploy

WOCHE 4:
- [ ] Launch auf Twitter
- [ ] Creator Beta-Tester
```

### Pricing
| Tier | Preis | Features |
|------|-------|----------|
| Free | 0€ | 5 Generierungen/Tag |
| Pro | 9.99€/mo | Unlimited + History |
| Team | 29.99€/mo | 5 Seats + Brand Presets |

### Marketing
1. **Build in Public**: Tweet jeden Fortschritt
2. **Creator Collabs**: Gratis Pro für Reviews
3. **Before/After Content**: Zeit-Ersparnis zeigen

---

## Brief 3: LocalBot

**Tagline:** Dein AI-Sekretariat für 24/7 Kundenservice

### Problem
Kleine Businesses (Cafés, Studios, Shops) bekommen ständig die gleichen Fragen: Öffnungszeiten, Preise, Termine. Zeit für persönliche Antworten fehlt.

### Lösung
WhatsApp/Instagram Bot der FAQ beantwortet, Termine vereinbart und Google Reviews beantwortet.

### Zielgruppe
- Lokale Businesses mit 1-10 Mitarbeitern
- Besonders: Friseure, Fitnessstudios, Restaurants, Handwerker

### Tech Stack
```
Backend:
- Python + FastAPI
- Twilio (WhatsApp)
- OpenAI API
- Supabase (Daten)

Optional:
- Calendly/Cal.com Integration
- Google Business API
```

### Features MVP
1. WhatsApp Bot (FAQ beantworten)
2. Öffnungszeiten + Preise aus Config
3. Termin-Link senden
4. Admin Dashboard (Logs, Stats)

### Features Later
- Google Reviews Auto-Reply
- Instagram DM Bot
- Mehrsprachigkeit
- Voice Messages verstehen

### Roadmap
```
WOCHE 1:
- [ ] 3-5 lokale Businesses befragen
- [ ] Twilio Setup + Test
- [ ] FAQ Prompt optimieren

WOCHE 2:
- [ ] Bot Grundfunktionen
- [ ] Admin Dashboard
- [ ] Test mit 1-2 echten Businesses

WOCHE 3:
- [ ] Termin-Integration
- [ ] Error Handling
- [ ] Deploy

WOCHE 4:
- [ ] Beta Launch mit 5 Businesses
- [ ] Feedback sammeln
- [ ] Pricing validieren
```

### Pricing
| Tier | Preis | Features |
|------|-------|----------|
| Starter | 29€/mo | 500 Nachrichten |
| Pro | 79€/mo | 2000 Nachrichten + Analytics |
| Enterprise | 199€/mo | Unlimited + Custom |

### Marketing
1. **Lokal denken**: Flyern bei Businesses
2. **Case Study**: Ein Business dokumentieren
3. **ROI zeigen**: "Spart 10h/Woche"
4. **Empfehlungsprogramm**: 1 Monat gratis pro Referral

---

## Brief 4: JobCraft

**Tagline:** Bewirb dich wie ein Startup

### Problem
Bewerbungen sind zeitaufwändig. Für jede Stelle: CV anpassen, Anschreiben neu schreiben, Research zur Firma machen.

### Lösung
AI die CV + Stellenausschreibung analysiert und perfekt angepasste Bewerbungsunterlagen generiert.

### Zielgruppe
- Berufseinsteiger
- Karrierewechsler
- Vielbewerber

### Tech Stack
```
Backend:
- Python + FastAPI
- Claude API (gut für lange Texte)
- PDF Parsing für CV

Frontend:
- Next.js
- Rich Text Editor

Infra:
- Vercel + Railway
```

### Features MVP
1. CV Upload (PDF)
2. Job URL eingeben (scrapen)
3. Anschreiben generieren
4. CV Highlights für diese Stelle

### Features Later
- Interview-Prep (Fragen üben)
- LinkedIn Message Generator
- Salary Negotiation Tips
- Application Tracker

### Roadmap
```
WOCHE 1:
- [ ] CV Parser bauen
- [ ] Job Posting Scraper
- [ ] Prompt für Anschreiben

WOCHE 2:
- [ ] UI mit Preview
- [ ] Export als PDF
- [ ] 10 Test-Bewerbungen

WOCHE 3:
- [ ] User Accounts
- [ ] History
- [ ] Deploy

WOCHE 4:
- [ ] Launch auf LinkedIn
- [ ] Unis/Career Centers kontaktieren
```

### Pricing
| Tier | Preis | Features |
|------|-------|----------|
| Free | 0€ | 3 Bewerbungen |
| Pro | 9.99€/mo | Unlimited |
| Lifetime | 49€ einmalig | Unlimited forever |

---

## Brief 5: EcoRadar

**Tagline:** Shop nachhaltig, ohne zu suchen

### Problem
Konsument:innen wollen nachhaltiger kaufen, aber es ist schwer herauszufinden welche Produkte wirklich gut sind.

### Lösung
AI die Produkte analysiert, CO2-Impact schätzt und nachhaltige Alternativen vorschlägt.

### Zielgruppe
- Umweltbewusste Shopper (18-35)
- Nachhaltigkeits-Blogger/Influencer

### Tech Stack
```
Backend:
- Python + FastAPI
- Web Scraping (Playwright)
- OpenAI für Analyse
- Supabase

Frontend:
- Next.js
- oder Chrome Extension

Data:
- Produkt-Datenbanken
- CO2-Schätzungen
```

### Features MVP
1. Produkt-URL eingeben
2. Nachhaltigkeits-Score
3. 3 bessere Alternativen

### Features Later
- Browser Extension
- Barcode Scanner (Mobile)
- Brand Rankings
- Affiliate Integration

### Roadmap
```
WOCHE 1:
- [ ] Research: Nachhaltigkeits-Kriterien
- [ ] Scraping von 3 großen Shops
- [ ] Scoring-System definieren

WOCHE 2:
- [ ] Analyse-Pipeline
- [ ] Alternativen-Matching
- [ ] Basic UI

WOCHE 3:
- [ ] 100 Produkte testen
- [ ] Accuracy verbessern
- [ ] Deploy

WOCHE 4:
- [ ] Launch bei Sustainability Communities
- [ ] Influencer Outreach
```

### Pricing
| Tier | Preis | Features |
|------|-------|----------|
| Free | 0€ | 10 Scans/Tag |
| Pro | 4.99€/mo | Unlimited |
| B2B | Custom | API Access für Shops |

### Revenue Streams
1. Subscription
2. Affiliate Links zu nachhaltigen Produkten
3. B2B API für E-Commerce Shops

---

## Brief 6: EventAI

**Tagline:** Plane Parties wie ein Pro

### Problem
Events planen ist stressig: Budget, Location, Essen, Musik, Einladungen – alles muss koordiniert werden.

### Lösung
AI-Assistent der bei der kompletten Event-Planung hilft: Budget, Checklisten, Einkaufslisten, Playlist-Vorschläge, Promo-Texte.

### Zielgruppe
- Student Clubs
- Private Party-Hosts
- Kleine Event-Agenturen

### Tech Stack
```
Backend:
- Python + FastAPI
- Llama 3 via Ollama (günstiger für viele Anfragen)
- oder OpenAI

Frontend:
- Next.js
- Checklist-UI

Integrations:
- Spotify API (Playlists)
- Optional: Notion Export
```

### Features MVP
1. Event-Brief eingeben (Art, Budget, Gäste)
2. Automatische Checkliste
3. Einkaufsliste
4. Timeline

### Features Later
- Playlist Generator (Spotify)
- Einladungs-Templates
- Budget Tracker
- Vendor Empfehlungen

### Roadmap
```
WOCHE 1:
- [ ] Event-Typen definieren (Party, Meetup, Konferenz)
- [ ] Checklisten-Templates
- [ ] Prompt Engineering

WOCHE 2:
- [ ] Generierung funktioniert
- [ ] UI mit Drag&Drop Checkliste
- [ ] Export Optionen

WOCHE 3:
- [ ] Spotify Integration
- [ ] Test mit 3 echten Events
- [ ] Deploy

WOCHE 4:
- [ ] Launch in Student Groups
- [ ] Templates als Freebies teilen
```

### Pricing
| Tier | Preis | Features |
|------|-------|----------|
| Free | 0€ | 1 Event/Monat |
| Pro | 7.99€/mo | Unlimited Events |
| Club | 19.99€/mo | Team + Branding |

---

## Projekt-Auswahl Guide

### Nach Schwierigkeit

| Projekt | Schwierigkeit | Wochen bis MVP |
|---------|---------------|----------------|
| ContentForge | ⭐ | 2 |
| EventAI | ⭐ | 2-3 |
| JobCraft | ⭐⭐ | 3 |
| StudyBuddy | ⭐⭐ | 3-4 |
| LocalBot | ⭐⭐⭐ | 4 |
| EcoRadar | ⭐⭐⭐ | 4-5 |

### Nach Monetarisierung

| Projekt | B2C/B2B | Revenue Potential |
|---------|---------|-------------------|
| LocalBot | B2B | €€€ (höhere Preise) |
| JobCraft | B2C | €€ (viele User möglich) |
| StudyBuddy | B2C | €€ |
| ContentForge | B2C | €€ |
| EcoRadar | B2C + B2B | € bis €€€ |
| EventAI | B2C | € |

### Nach Tech-Stack

| Projekt | Haupt-Skills |
|---------|--------------|
| StudyBuddy | RAG, PDF Parsing |
| ContentForge | Prompt Engineering |
| LocalBot | APIs, Webhooks |
| JobCraft | Scraping, Text Gen |
| EcoRadar | Scraping, Analyse |
| EventAI | Templates, Lists |

---

## Nächste Schritte

1. **Wähle EIN Projekt** (nicht drei)
2. **Validiere das Problem** (5-10 Gespräche)
3. **Baue den kleinsten MVP** (nicht alle Features)
4. **Launch in 4 Wochen** (nicht 4 Monaten)
5. **Iterate basierend auf Feedback**

Das perfekte Projekt existiert nicht. Wähle eins und STARTE.
