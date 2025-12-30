# Infrastruktur Playbook - GenZAI

Alles was du brauchst um Cloud Computing zu verstehen und von "läuft auf meinem Laptop" zu "läuft im Internet" zu kommen. Dieses Playbook deckt auch die Grundlagen ab, die du für Zertifizierungen wie **AZ-900 (Azure Fundamentals)** brauchst.

---

### Legende

![AZ-900](https://learn.microsoft.com/en-us/media/learn/certification/badges/microsoft-certified-fundamentals-badge.svg) **AZ-900** = Dieses Kapitel ist relevant für die Microsoft Azure Fundamentals Zertifizierung

---

# TEIL 1: CLOUD COMPUTING GRUNDLAGEN

---

## Kapitel 1: Was ist Cloud Computing? ![AZ-900](https://learn.microsoft.com/en-us/media/learn/certification/badges/microsoft-certified-fundamentals-badge.svg)

### Die Simple Erklärung

**Cloud Computing** = Computer-Ressourcen (Server, Storage, Datenbanken, etc.) über das Internet mieten statt kaufen.

```
Früher (On-Premises):
┌─────────────────────────────────────────┐
│  Deine Firma                            │
│  ┌─────────────────────────────────┐    │
│  │  Eigener Serverraum             │    │
│  │  - Server kaufen ($$$$)         │    │
│  │  - Strom zahlen                 │    │
│  │  - IT-Team einstellen           │    │
│  │  - Klimaanlage                  │    │
│  │  - Sicherheit                   │    │
│  └─────────────────────────────────┘    │
└─────────────────────────────────────────┘

Heute (Cloud):
┌─────────────────┐         ┌─────────────────┐
│  Deine Firma    │ ──────> │  Cloud Provider │
│  - Laptop       │ Internet│  - Rechenzentren│
│  - Internet     │         │  - Server       │
│                 │         │  - Storage      │
│  Miete was du   │         │  - Alles managed│
│  brauchst       │         │                 │
└─────────────────┘         └─────────────────┘
```

### Warum Cloud? Die 6 Vorteile

| Vorteil | Erklärung | Real-World Beispiel |
|---------|-----------|---------------------|
| **1. Keine Vorabkosten** | Kein Server kaufen, pay-as-you-go | Startup startet mit 10€/Monat statt 10.000€ Server |
| **2. Skalierbarkeit** | Mehr Power wenn nötig, weniger wenn nicht | Black Friday: 100x mehr Server, danach wieder runter |
| **3. Elastizität** | Automatisch hoch/runterskalieren | Viral TikTok → Auto-Scale → kein Crash |
| **4. Globale Reichweite** | Server überall auf der Welt | App in Frankfurt UND Tokyo deployen |
| **5. Hochverfügbarkeit** | Läuft auch wenn Hardware stirbt | Server crashed → automatisch neuer Server |
| **6. Schnelligkeit** | Neue Server in Minuten, nicht Wochen | Idee → Deploy in 10 Minuten |

### CapEx vs OpEx (Wichtig für AZ-900!)

```
CapEx (Capital Expenditure) = KAUFEN
────────────────────────────────────
- Einmalige große Ausgabe
- Server, Hardware, Gebäude
- Abschreibung über Jahre
- Eigentum der Firma

Beispiel: Server für 10.000€ kaufen
         → 5 Jahre nutzen
         → 2.000€/Jahr Abschreibung

OpEx (Operational Expenditure) = MIETEN
────────────────────────────────────────
- Laufende monatliche Kosten
- Cloud-Subscriptions, Miete
- Sofort als Ausgabe verbucht
- Flexibel skalierbar

Beispiel: Cloud-Server für 100€/Monat
         → Jederzeit kündbar
         → Mehr/weniger buchen
```

**Cloud = OpEx-Modell** → Weniger Risiko, mehr Flexibilität

---

## Kapitel 2: Cloud Service-Modelle (IaaS, PaaS, SaaS) ![AZ-900](https://learn.microsoft.com/en-us/media/learn/certification/badges/microsoft-certified-fundamentals-badge.svg)

### Das Pizza-Modell 🍕

```
                    Was DU machst vs. was der PROVIDER macht

┌─────────────────────────────────────────────────────────────────────┐
│                                                                      │
│   ON-PREMISES     IaaS          PaaS          SaaS                  │
│   (Selbst)        (Infra)       (Plattform)   (Software)            │
│                                                                      │
│   ┌─────────┐    ┌─────────┐    ┌─────────┐   ┌─────────┐          │
│   │ App     │    │ App     │    │ App     │   │░░░░░░░░░│ Provider │
│   ├─────────┤    ├─────────┤    ├─────────┤   ├─────────┤          │
│   │ Data    │    │ Data    │    │░░░░░░░░░│   │░░░░░░░░░│ Provider │
│   ├─────────┤    ├─────────┤    ├─────────┤   ├─────────┤          │
│   │ Runtime │    │ Runtime │    │░░░░░░░░░│   │░░░░░░░░░│ Provider │
│   ├─────────┤    ├─────────┤    ├─────────┤   ├─────────┤          │
│   │ OS      │    │ OS      │    │░░░░░░░░░│   │░░░░░░░░░│ Provider │
│   ├─────────┤    ├─────────┤    ├─────────┤   ├─────────┤          │
│   │ Server  │    │░░░░░░░░░│    │░░░░░░░░░│   │░░░░░░░░░│ Provider │
│   ├─────────┤    ├─────────┤    ├─────────┤   ├─────────┤          │
│   │ Storage │    │░░░░░░░░░│    │░░░░░░░░░│   │░░░░░░░░░│ Provider │
│   ├─────────┤    ├─────────┤    ├─────────┤   ├─────────┤          │
│   │ Network │    │░░░░░░░░░│    │░░░░░░░░░│   │░░░░░░░░░│ Provider │
│   └─────────┘    └─────────┘    └─────────┘   └─────────┘          │
│                                                                      │
│   Selbst Pizza   Tiefkühlpizza  Lieferservice Restaurant           │
│   machen         aufbacken      bestellen     essen gehen           │
│                                                                      │
└─────────────────────────────────────────────────────────────────────┘
```

### IaaS - Infrastructure as a Service

**Du mietest:** Virtuelle Maschinen, Storage, Netzwerk
**Du machst:** OS installieren, Software einrichten, alles konfigurieren

```
Beispiele:
- Azure Virtual Machines
- AWS EC2
- Google Compute Engine
- Hetzner Cloud
- DigitalOcean Droplets

Wann nutzen?
✓ Volle Kontrolle gebraucht
✓ Spezielle Software-Anforderungen
✓ Legacy-Apps migrieren
✓ Du weißt was du tust

Für AI-Projekte:
→ GPU-VMs für eigenes Model Training
→ Eigene RAG-Infrastruktur
→ Self-hosted LLMs (Llama, Mistral)
```

### PaaS - Platform as a Service

**Du mietest:** Komplette Plattform zum Entwickeln
**Du machst:** Nur deinen Code schreiben und deployen

```
Beispiele:
- Azure App Service
- AWS Elastic Beanstalk
- Google App Engine
- Heroku
- Railway
- Render

Wann nutzen?
✓ Schnell deployen ohne Server-Stress
✓ Fokus auf Code, nicht Infrastruktur
✓ Auto-Scaling gewünscht
✓ Team ohne DevOps-Expertise

Für AI-Projekte:
→ FastAPI-Backend mit OpenAI-Integration
→ RAG-Apps mit managed Vektor-DBs
→ Chatbot-APIs
```

### SaaS - Software as a Service

**Du mietest:** Fertige Software über Browser/API
**Du machst:** Nur benutzen

```
Beispiele:
- Microsoft 365
- Google Workspace
- Salesforce
- Slack, Notion, Figma
- OpenAI API (!)
- ChatGPT Plus

Wann nutzen?
✓ Standard-Software reicht
✓ Keine Entwicklung nötig
✓ Sofort loslegen

Für AI-Projekte:
→ OpenAI/Anthropic APIs = SaaS!
→ Du baust keine LLMs, du NUTZT sie
→ Pinecone, Weaviate Cloud = SaaS Vector DBs
```

### Vergleich auf einen Blick

| Aspekt | IaaS | PaaS | SaaS |
|--------|------|------|------|
| **Kontrolle** | Hoch | Mittel | Niedrig |
| **Flexibilität** | Hoch | Mittel | Niedrig |
| **Management-Aufwand** | Hoch | Niedrig | Keiner |
| **Kosten** | Variabel | Mittel | Fix/User |
| **Setup-Zeit** | Stunden | Minuten | Sofort |
| **Beispiel** | Hetzner VM | Railway | ChatGPT |

### Shared Responsibility Model

Wichtig zu verstehen: **Wer ist wofür verantwortlich?**

```
                        On-Prem    IaaS     PaaS     SaaS
                        ───────    ────     ────     ────
Daten & Zugang            DU        DU       DU       DU
Identität & Accounts      DU        DU       DU       DU
Anwendungen               DU        DU       DU     Provider
Netzwerk-Kontrolle        DU        DU     Geteilt  Provider
OS                        DU        DU     Provider Provider
Physische Hosts           DU     Provider  Provider Provider
Physisches Netzwerk       DU     Provider  Provider Provider
Physisches Datacenter     DU     Provider  Provider Provider
```

**Merke:** Auch in der Cloud bist DU für deine Daten und Zugänge verantwortlich!

---

## Kapitel 3: Cloud-Deployment-Modelle ![AZ-900](https://learn.microsoft.com/en-us/media/learn/certification/badges/microsoft-certified-fundamentals-badge.svg)

### Public Cloud

```
┌──────────────────────────────────────────────┐
│              PUBLIC CLOUD                     │
│                                               │
│  ┌─────────┐ ┌─────────┐ ┌─────────┐        │
│  │ Firma A │ │ Firma B │ │ Firma C │        │
│  └────┬────┘ └────┬────┘ └────┬────┘        │
│       │           │           │              │
│       └───────────┼───────────┘              │
│                   ▼                          │
│         ┌─────────────────┐                  │
│         │  Shared Infra   │                  │
│         │  (Azure, AWS)   │                  │
│         └─────────────────┘                  │
│                                               │
│  ✓ Jeder kann es nutzen                      │
│  ✓ Pay-per-use                               │
│  ✓ Keine Hardware-Kosten                     │
│  ✓ Schnell skalierbar                        │
│                                               │
│  Beispiele: Azure, AWS, GCP, Hetzner         │
└──────────────────────────────────────────────┘
```

### Private Cloud

```
┌──────────────────────────────────────────────┐
│              PRIVATE CLOUD                    │
│                                               │
│  ┌─────────────────────────────────────┐     │
│  │           NUR DEINE FIRMA           │     │
│  │                                     │     │
│  │  ┌──────────────────────────────┐  │     │
│  │  │     Eigenes Datacenter       │  │     │
│  │  │     ODER                     │  │     │
│  │  │     Dedicated Cloud          │  │     │
│  │  └──────────────────────────────┘  │     │
│  │                                     │     │
│  └─────────────────────────────────────┘     │
│                                               │
│  ✓ Volle Kontrolle                           │
│  ✓ Compliance-freundlich                     │
│  ✓ Maximale Sicherheit                       │
│  ✗ Teurer                                    │
│  ✗ Mehr Management                           │
│                                               │
│  Beispiele: Azure Stack, VMware, OpenStack   │
│  Wer nutzt es: Banken, Behörden, Gesundheit  │
└──────────────────────────────────────────────┘
```

### Hybrid Cloud

```
┌──────────────────────────────────────────────┐
│              HYBRID CLOUD                     │
│                                               │
│  ┌───────────────┐      ┌───────────────┐   │
│  │ Private Cloud │◄────►│ Public Cloud  │   │
│  │ (On-Premises) │      │ (Azure/AWS)   │   │
│  │               │      │               │   │
│  │ Sensible      │      │ Weniger       │   │
│  │ Daten         │      │ sensible      │   │
│  │               │      │ Workloads     │   │
│  └───────────────┘      └───────────────┘   │
│                                               │
│  ✓ Best of both worlds                       │
│  ✓ Flexibel                                  │
│  ✓ Schrittweise Migration                    │
│  ✗ Komplexer zu managen                      │
│                                               │
│  Beispiel: Kundendaten lokal, AI in Cloud    │
└──────────────────────────────────────────────┘
```

### Multi-Cloud

```
┌──────────────────────────────────────────────┐
│              MULTI-CLOUD                      │
│                                               │
│      ┌─────────┐ ┌─────────┐ ┌─────────┐    │
│      │  Azure  │ │   AWS   │ │   GCP   │    │
│      └────┬────┘ └────┬────┘ └────┬────┘    │
│           │           │           │          │
│           └───────────┼───────────┘          │
│                       ▼                      │
│              ┌─────────────┐                 │
│              │ Deine Apps  │                 │
│              └─────────────┘                 │
│                                               │
│  ✓ Kein Vendor Lock-in                       │
│  ✓ Best-of-breed Services                    │
│  ✓ Redundanz                                 │
│  ✗ Sehr komplex                              │
│  ✗ Braucht viel Expertise                    │
│                                               │
│  Wer macht das: Große Enterprises            │
└──────────────────────────────────────────────┘
```

### Welches Modell für dich?

```
Startup/Side Project     → Public Cloud (Azure, Hetzner)
Sensible Daten (DSGVO)   → Private oder Hybrid
Enterprise               → Hybrid oder Multi-Cloud
AI-Projekte              → Public Cloud (99% der Fälle)
```

---

## Kapitel 4: Virtualisierung Deep Dive ![AZ-900](https://learn.microsoft.com/en-us/media/learn/certification/badges/microsoft-certified-fundamentals-badge.svg)

### Was ist Virtualisierung?

**Virtualisierung** = Ein physischer Computer tut so, als wäre er mehrere Computer.

```
OHNE Virtualisierung:
┌─────────────────────────────────────┐
│        Physischer Server            │
│  ┌───────────────────────────────┐  │
│  │       1 Betriebssystem        │  │
│  │       1 Anwendung             │  │
│  │                               │  │
│  │   💰 Ressourcen verschwendet  │  │
│  │   (Server nur 10% ausgelastet)│  │
│  └───────────────────────────────┘  │
└─────────────────────────────────────┘

MIT Virtualisierung:
┌─────────────────────────────────────┐
│        Physischer Server            │
│  ┌─────────┐ ┌─────────┐ ┌───────┐ │
│  │  VM 1   │ │  VM 2   │ │ VM 3  │ │
│  │ Ubuntu  │ │ Windows │ │ Debian│ │
│  │ Web-App │ │ DB      │ │ AI    │ │
│  └─────────┘ └─────────┘ └───────┘ │
│  ┌───────────────────────────────┐  │
│  │         HYPERVISOR            │  │
│  └───────────────────────────────┘  │
│  ┌───────────────────────────────┐  │
│  │      Hardware (CPU, RAM)      │  │
│  └───────────────────────────────┘  │
│                                     │
│   ✓ Bessere Auslastung (80%+)      │
│   ✓ Isolation zwischen VMs         │
│   ✓ Verschiedene OS gleichzeitig   │
└─────────────────────────────────────┘
```

### Der Hypervisor

Der **Hypervisor** ist die Software, die VMs ermöglicht. Es gibt zwei Typen:

```
TYP 1 - Bare Metal (direkt auf Hardware)
──────────────────────────────────────────
┌─────────┐ ┌─────────┐ ┌─────────┐
│  VM 1   │ │  VM 2   │ │  VM 3   │
└────┬────┘ └────┬────┘ └────┬────┘
     └───────────┼───────────┘
                 ▼
    ┌─────────────────────────┐
    │   Hypervisor (Typ 1)    │
    │   VMware ESXi, Hyper-V  │
    │   Xen, KVM              │
    └─────────────────────────┘
                 ▼
    ┌─────────────────────────┐
    │       Hardware          │
    └─────────────────────────┘

→ Für Server/Cloud-Provider
→ Beste Performance
→ Azure/AWS nutzen das


TYP 2 - Hosted (auf einem OS)
──────────────────────────────────────────
┌─────────┐ ┌─────────┐ ┌─────────┐
│  VM 1   │ │  VM 2   │ │ Andere  │
└────┬────┘ └────┬────┘ │  Apps   │
     └───────────┼───────────┘
                 ▼
    ┌─────────────────────────┐
    │   Hypervisor (Typ 2)    │
    │   VirtualBox, VMware    │
    │   Workstation, Parallels│
    └─────────────────────────┘
                 ▼
    ┌─────────────────────────┐
    │  Host OS (Windows/Mac)  │
    └─────────────────────────┘
                 ▼
    ┌─────────────────────────┐
    │       Hardware          │
    └─────────────────────────┘

→ Für Entwickler/Testen
→ Einfach zu nutzen
→ Weniger Performance
```

### VMs vs Container

```
Virtual Machines                    Container
──────────────────                  ──────────────────
┌─────────┐ ┌─────────┐            ┌─────────┐ ┌─────────┐
│  App A  │ │  App B  │            │  App A  │ │  App B  │
├─────────┤ ├─────────┤            └────┬────┘ └────┬────┘
│  Libs   │ │  Libs   │                 │           │
├─────────┤ ├─────────┤            ┌────┴───────────┴────┐
│Guest OS │ │Guest OS │            │   Container Runtime │
│(Ubuntu) │ │(Debian) │            │      (Docker)       │
└────┬────┘ └────┬────┘            └──────────┬──────────┘
     └─────┬─────┘                            │
           ▼                                  ▼
┌─────────────────────┐            ┌─────────────────────┐
│     Hypervisor      │            │       Host OS       │
└─────────────────────┘            └─────────────────────┘

Größe: GBs                         Größe: MBs
Start: Minuten                     Start: Sekunden
Isolation: Stark                   Isolation: Schwächer
Use Case: Verschiedene OS          Use Case: Microservices
```

### CPU, RAM, Storage - Was du mietest

**vCPU (Virtual CPU)**
```
1 vCPU ≈ 1 Thread eines physischen CPU-Kerns
- Nicht ein ganzer Kern, sondern Zeit darauf
- "Shared" = andere VMs teilen sich die CPU
- "Dedicated" = garantierte CPU-Zeit

Für AI-Projekte:
- API-Server: 1-2 vCPU reichen
- RAG mit vielen Requests: 4+ vCPU
- Model Inference (lokal): 8+ vCPU oder GPU
```

**RAM**
```
RAM = Arbeitsspeicher der VM
- Mehr RAM = mehr gleichzeitige Operationen
- RAG-Systeme: 4-8 GB minimum
- Embedding-Models lokal: 8-16 GB
- LLMs lokal: 16-64 GB

Faustregel:
- Simple API: 2 GB
- RAG-App: 4-8 GB
- Production: 8-16 GB
```

**Storage**
```
Typen:
- SSD (Standard): Schnell, für OS + Apps
- NVMe SSD: Sehr schnell, für Datenbanken
- HDD: Langsam, günstig, für Backups/Archive

Für AI-Projekte:
- OS + Docker: 20-40 GB
- Vector DB (klein): 10-20 GB
- Dokumente für RAG: Je nach Menge
- Empfehlung Start: 80 GB SSD
```

---

## Kapitel 5: Cloud-Konzepte für Zuverlässigkeit ![AZ-900](https://learn.microsoft.com/en-us/media/learn/certification/badges/microsoft-certified-fundamentals-badge.svg)

### High Availability (HA)

**Hochverfügbarkeit** = System läuft auch wenn Teile ausfallen

```
OHNE HA:
┌─────────────┐
│  1 Server   │  ──── Server stirbt ──── 💀 App down
└─────────────┘

MIT HA:
┌─────────────┐    ┌─────────────┐
│  Server 1   │    │  Server 2   │
└──────┬──────┘    └──────┬──────┘
       │                  │
       └────────┬─────────┘
                ▼
        ┌──────────────┐
        │ Load Balancer│
        └──────────────┘
                │
    Server 1 stirbt? → Load Balancer schickt
                        Traffic zu Server 2
                     → User merkt nichts
```

**Availability in Prozent:**
```
99%      = 3.65 Tage Downtime/Jahr    (nicht gut)
99.9%    = 8.76 Stunden Downtime/Jahr (okay)
99.99%   = 52 Minuten Downtime/Jahr   (gut)
99.999%  = 5 Minuten Downtime/Jahr    (sehr gut)

Azure SLA Beispiele:
- VMs (einzeln): 99.9%
- VMs (Availability Set): 99.95%
- VMs (Availability Zones): 99.99%
```

### Skalierbarkeit

**Vertical Scaling (Scale Up/Down)**
```
┌─────────────┐         ┌─────────────────────┐
│   2 vCPU    │   →→→   │      8 vCPU         │
│   4 GB RAM  │         │     32 GB RAM       │
│   Kleine VM │         │    Größere VM       │
└─────────────┘         └─────────────────────┘

✓ Einfach
✓ Keine Code-Änderungen
✗ Hat Limits (max. VM-Größe)
✗ Downtime beim Upgrade
```

**Horizontal Scaling (Scale Out/In)**
```
┌─────────┐         ┌─────────┐ ┌─────────┐ ┌─────────┐
│   VM    │   →→→   │   VM    │ │   VM    │ │   VM    │
└─────────┘         └─────────┘ └─────────┘ └─────────┘

✓ Theoretisch unbegrenzt
✓ Bessere Verfügbarkeit
✗ App muss "stateless" sein
✗ Komplexer (Load Balancer etc.)
```

### Elastizität

**Elastizität** = Automatisch skalieren basierend auf Bedarf

```
Traffic-Muster:
                    ┌───┐
                    │   │
              ┌─────┤   ├─────┐
              │     │   │     │
        ┌─────┤     │   │     ├─────┐
────────┤     │     │   │     │     ├────────
   Nacht      Morgen    Mittag      Abend

Ohne Elastizität:
────────────────────────────────────────────── (Feste Kapazität)
        ▲ Verschwendet Geld wenn wenig Traffic
        ▼ Zu wenig Kapazität bei Spitzen

Mit Elastizität:
                    ┌───┐
              ┌─────┤   ├─────┐
        ┌─────┤     │   │     ├─────┐
────────┤     │     │   │     │     ├────────
        ↑ Automatisch mehr Server
        ↓ Automatisch weniger Server
```

### Fault Tolerance & Disaster Recovery

**Fault Tolerance** = System funktioniert trotz Fehlern
```
- Redundante Komponenten
- Automatisches Failover
- Kein Datenverlust bei Hardware-Ausfall
```

**Disaster Recovery** = Wiederherstellung nach Katastrophe
```
RPO (Recovery Point Objective):
→ Wie viel Datenverlust ist akzeptabel?
→ "Maximal 1 Stunde Daten verlieren"

RTO (Recovery Time Objective):
→ Wie schnell muss System wieder laufen?
→ "Innerhalb von 4 Stunden wieder online"

Strategien:
- Backup & Restore: Günstig, langsam (Stunden)
- Pilot Light: Minimal-System läuft immer (Minuten)
- Hot Standby: Volle Kopie läuft parallel (Sekunden)
```

---

## Kapitel 6: Azure-Grundlagen ![AZ-900](https://learn.microsoft.com/en-us/media/learn/certification/badges/microsoft-certified-fundamentals-badge.svg)

### Azure Geographie

```
┌─────────────────────────────────────────────────────────────┐
│                        GEOGRAPHY                             │
│                    (z.B. "Europe")                          │
│                                                              │
│   ┌───────────────────────────────────────────────────┐     │
│   │                    REGION                          │     │
│   │               (z.B. "West Europe")                 │     │
│   │                                                    │     │
│   │   ┌─────────────────────────────────────────┐    │     │
│   │   │         AVAILABILITY ZONE 1              │    │     │
│   │   │   ┌─────────┐  ┌─────────┐              │    │     │
│   │   │   │Datacenter│ │Datacenter│              │    │     │
│   │   │   └─────────┘  └─────────┘              │    │     │
│   │   └─────────────────────────────────────────┘    │     │
│   │                                                    │     │
│   │   ┌─────────────────────────────────────────┐    │     │
│   │   │         AVAILABILITY ZONE 2              │    │     │
│   │   │   ┌─────────┐  ┌─────────┐              │    │     │
│   │   │   │Datacenter│ │Datacenter│              │    │     │
│   │   │   └─────────┘  └─────────┘              │    │     │
│   │   └─────────────────────────────────────────┘    │     │
│   │                                                    │     │
│   │   ┌─────────────────────────────────────────┐    │     │
│   │   │         AVAILABILITY ZONE 3              │    │     │
│   │   │   ┌─────────┐  ┌─────────┐              │    │     │
│   │   │   │Datacenter│ │Datacenter│              │    │     │
│   │   │   └─────────┘  └─────────┘              │    │     │
│   │   └─────────────────────────────────────────┘    │     │
│   │                                                    │     │
│   └───────────────────────────────────────────────────┘     │
│                                                              │
└─────────────────────────────────────────────────────────────┘

Geographies:     Americas, Europe, Asia Pacific, etc.
Regions:         West Europe, Germany West Central, etc.
Avail. Zones:    Physisch getrennte Datacenter in einer Region
Region Pairs:    Zwei Regions für Disaster Recovery (z.B. West Europe ↔ North Europe)
```

### Azure Ressourcen-Hierarchie

```
┌─────────────────────────────────────────────┐
│             Management Group                 │
│        (Optional, für große Firmen)          │
└──────────────────────┬──────────────────────┘
                       │
                       ▼
┌─────────────────────────────────────────────┐
│              Subscription                    │
│     (Abrechnungseinheit, z.B. "Prod")       │
└──────────────────────┬──────────────────────┘
                       │
         ┌─────────────┴─────────────┐
         ▼                           ▼
┌─────────────────┐         ┌─────────────────┐
│ Resource Group  │         │ Resource Group  │
│   "rg-api-prod" │         │  "rg-db-prod"   │
└────────┬────────┘         └────────┬────────┘
         │                           │
    ┌────┴────┐                 ┌────┴────┐
    ▼         ▼                 ▼         ▼
┌──────┐  ┌──────┐         ┌──────┐  ┌──────┐
│ VM   │  │ App  │         │ SQL  │  │Storage│
│      │  │Service│        │ DB   │  │      │
└──────┘  └──────┘         └──────┘  └──────┘
```

### Wichtige Azure Services

**Compute:**
```
Azure Virtual Machines    → IaaS, volle Kontrolle
Azure App Service        → PaaS, Web Apps easy deployen
Azure Functions          → Serverless, pay-per-execution
Azure Kubernetes (AKS)   → Container Orchestration
Azure Container Instance → Container ohne Cluster
```

**Storage:**
```
Blob Storage             → Unstrukturierte Daten (Files, Images)
File Storage             → Shared File System (SMB)
Queue Storage            → Message Queues
Table Storage            → NoSQL Key-Value
Disk Storage             → VHDs für VMs
```

**Datenbank:**
```
Azure SQL Database       → Managed SQL Server
Cosmos DB               → Global verteilte NoSQL
Azure Database for      → Managed PostgreSQL/MySQL
Azure Cache for Redis   → In-Memory Caching
```

**AI & ML:**
```
Azure OpenAI Service    → GPT-4, DALL-E, etc.
Azure Machine Learning  → ML Plattform
Cognitive Services      → Vision, Speech, Language APIs
Azure AI Search         → Vektor-Suche für RAG
```

**Netzwerk:**
```
Virtual Network (VNet)  → Isoliertes Netzwerk
Load Balancer          → Traffic verteilen
Application Gateway    → Layer 7 Load Balancer
Azure CDN              → Content Delivery Network
Azure DNS              → DNS Hosting
```

### Azure Kostenmodell

```
Faktoren die Kosten beeinflussen:
──────────────────────────────────
1. Resource Type       → VM teurer als Storage
2. Usage              → Pay-per-use
3. Region             → West Europe ≠ East US
4. Tier               → Basic vs Standard vs Premium
5. Outbound Traffic   → Inbound free, Outbound kostet

Kosten sparen:
──────────────────────────────────
- Reserved Instances  → 1-3 Jahre committen = bis 72% sparen
- Spot VMs           → Unused Capacity = bis 90% sparen
- Auto-Shutdown      → Dev-VMs nachts aus
- Right-Sizing       → Nicht zu große VMs
- Azure Advisor      → Kostenlose Empfehlungen
```

### Azure Identität & Security

```
Azure Active Directory (Entra ID):
─────────────────────────────────
- Identity Provider für Azure
- Single Sign-On (SSO)
- Multi-Factor Authentication (MFA)
- Conditional Access Policies

RBAC (Role-Based Access Control):
─────────────────────────────────
- Owner        → Alles, inkl. Rechte vergeben
- Contributor  → Alles außer Rechte vergeben
- Reader       → Nur lesen
- Custom Roles → Eigene Rollen definieren

Prinzip: Least Privilege
→ Nur die Rechte geben, die gebraucht werden
```

---

## Kapitel 7: Azure Governance & Compliance ![AZ-900](https://learn.microsoft.com/en-us/media/learn/certification/badges/microsoft-certified-fundamentals-badge.svg)

### Azure Policy

**Azure Policy** = Regeln die automatisch durchgesetzt werden

```
Beispiele für Policies:
─────────────────────────────────
- "Nur VMs in West Europe erlaubt"
- "Storage muss verschlüsselt sein"
- "Keine Public IPs auf VMs"
- "Nur bestimmte VM-Größen erlaubt"
- "Tags sind Pflicht"

Was passiert bei Verstoß?
- Deny:     Ressource kann nicht erstellt werden
- Audit:    Warnung, aber erlaubt
- Modify:   Automatisch korrigieren
- DeployIfNotExists: Fehlende Ressource erstellen
```

### Azure Blueprints

**Blueprints** = Vorlagen für komplette Umgebungen

```
┌─────────────────────────────────────────────┐
│              AZURE BLUEPRINT                 │
│                                              │
│  ┌───────────────────────────────────────┐  │
│  │ Resource Groups                       │  │
│  │ + Policies                            │  │
│  │ + RBAC Assignments                    │  │
│  │ + ARM Templates                       │  │
│  │ + Artifacts                           │  │
│  └───────────────────────────────────────┘  │
│                                              │
│  1x definieren → beliebig oft anwenden      │
│                                              │
│  Beispiel: "Sichere Web-App Umgebung"       │
│  - Resource Group mit Tags                  │
│  - App Service + SQL Database               │
│  - Policies für Compliance                  │
│  - Reader-Rolle für Audit-Team              │
└─────────────────────────────────────────────┘
```

### Resource Locks

**Locks** = Schutz vor versehentlichem Löschen/Ändern

```
Lock-Typen:
───────────────────
ReadOnly:  Ressource kann nur gelesen werden
           (keine Änderungen, kein Löschen)

Delete:    Ressource kann geändert werden
           (aber nicht gelöscht)

Wann nutzen?
→ Production-Datenbanken
→ Wichtige VNets
→ Storage mit kritischen Daten

# Azure CLI Beispiel
az lock create --name "CanNotDelete" \
  --lock-type CanNotDelete \
  --resource-group myRG
```

### Tags

**Tags** = Metadaten für Ressourcen (Key-Value Pairs)

```
Typische Tags:
───────────────────────────────
environment: production / dev / staging
project: StudyBuddy
costcenter: IT-123
owner: max@firma.de
created: 2024-01-15

Warum Tags?
✓ Kosten nach Projekt filtern
✓ Ressourcen finden
✓ Automatisierung (z.B. Dev nachts aus)
✓ Compliance-Reporting

Azure Policy für Tags:
"Require a tag on resources" → Ohne Tag keine Erstellung
```

### Management Groups

**Management Groups** = Hierarchie über Subscriptions

```
┌─────────────────────────────────────────────────┐
│            Root Management Group                 │
│                                                  │
│   ┌─────────────────┐   ┌─────────────────┐    │
│   │ MG: Production  │   │ MG: Development │    │
│   │                 │   │                 │    │
│   │ ┌─────────────┐│   │ ┌─────────────┐│    │
│   │ │ Sub: Prod-EU││   │ │ Sub: Dev    ││    │
│   │ └─────────────┘│   │ └─────────────┘│    │
│   │ ┌─────────────┐│   │ ┌─────────────┐│    │
│   │ │ Sub: Prod-US││   │ │ Sub: Test   ││    │
│   │ └─────────────┘│   │ └─────────────┘│    │
│   └─────────────────┘   └─────────────────┘    │
│                                                  │
│   Policies auf MG-Level → gilt für alle         │
│   Subscriptions darunter!                       │
└─────────────────────────────────────────────────┘
```

---

## Kapitel 8: Azure Management Tools ![AZ-900](https://learn.microsoft.com/en-us/media/learn/certification/badges/microsoft-certified-fundamentals-badge.svg)

### Azure Portal

**Das Web-Interface** - portal.azure.com

```
Vorteile:
✓ Grafische Oberfläche
✓ Gut für Anfänger
✓ Schnelle Übersicht
✓ Dashboards anpassbar

Nachteile:
✗ Nicht automatisierbar
✗ Langsamer als CLI
✗ Klick-Fehler möglich
```

### Azure CLI

**Command Line Interface** - Terminal/PowerShell

```bash
# Installation
# Windows: winget install Microsoft.AzureCLI
# Mac: brew install azure-cli
# Linux: curl -sL https://aka.ms/InstallAzureCLIDeb | sudo bash

# Login
az login

# Subscription setzen
az account set --subscription "My Subscription"

# Resource Group erstellen
az group create --name myRG --location westeurope

# VM erstellen
az vm create \
  --resource-group myRG \
  --name myVM \
  --image Ubuntu2204 \
  --admin-username azureuser \
  --generate-ssh-keys

# Alle VMs auflisten
az vm list --output table
```

### Azure PowerShell

**Für Windows-Admins**

```powershell
# Installation
Install-Module -Name Az -Repository PSGallery -Force

# Login
Connect-AzAccount

# Resource Group erstellen
New-AzResourceGroup -Name myRG -Location "West Europe"

# VM erstellen
New-AzVM `
  -ResourceGroupName myRG `
  -Name myVM `
  -Location "West Europe" `
  -Image Ubuntu2204
```

### Azure Cloud Shell

**Browser-basierte Shell** - Direkt im Portal

```
Vorteile:
✓ Keine Installation nötig
✓ Immer aktuell
✓ CLI + PowerShell verfügbar
✓ Persistenter Storage (5 GB)
✓ Vorinstallierte Tools (git, kubectl, terraform)

Zugang:
→ portal.azure.com → Cloud Shell Icon (>_)
→ shell.azure.com
```

### ARM Templates (Infrastructure as Code)

**JSON-Vorlagen für Azure Ressourcen**

```json
{
  "$schema": "https://schema.management.azure.com/...",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "storageAccountName": {
      "type": "string"
    }
  },
  "resources": [
    {
      "type": "Microsoft.Storage/storageAccounts",
      "apiVersion": "2021-02-01",
      "name": "[parameters('storageAccountName')]",
      "location": "[resourceGroup().location]",
      "sku": {
        "name": "Standard_LRS"
      },
      "kind": "StorageV2"
    }
  ]
}
```

```
Vorteile von IaC:
✓ Wiederholbar
✓ Versionierbar (Git)
✓ Review-fähig
✓ Konsistente Umgebungen
✓ Dokumentation inklusive
```

### Bicep (Modernes IaC)

**Einfachere Alternative zu ARM JSON**

```bicep
// storage.bicep
param storageAccountName string
param location string = resourceGroup().location

resource storageAccount 'Microsoft.Storage/storageAccounts@2021-02-01' = {
  name: storageAccountName
  location: location
  sku: {
    name: 'Standard_LRS'
  }
  kind: 'StorageV2'
}

output storageEndpoint string = storageAccount.properties.primaryEndpoints.blob
```

```bash
# Deployment
az deployment group create \
  --resource-group myRG \
  --template-file storage.bicep \
  --parameters storageAccountName=mystorageacc
```

### Azure Arc

**Azure-Management für alles (auch On-Premises)**

```
┌─────────────────────────────────────────────┐
│                 AZURE ARC                    │
│                                              │
│  Managed Alles:                             │
│  ┌─────────┐ ┌─────────┐ ┌─────────┐       │
│  │ Azure   │ │ On-Prem │ │ Other   │       │
│  │ VMs     │ │ Server  │ │ Clouds  │       │
│  └─────────┘ └─────────┘ └─────────┘       │
│                                              │
│  → Einheitliches Management                 │
│  → Azure Policy auch für On-Prem            │
│  → Zentrales Monitoring                     │
└─────────────────────────────────────────────┘
```

---

## Kapitel 9: Azure Monitoring ![AZ-900](https://learn.microsoft.com/en-us/media/learn/certification/badges/microsoft-certified-fundamentals-badge.svg)

### Azure Monitor

**Zentrale Monitoring-Plattform**

```
┌─────────────────────────────────────────────────┐
│                 AZURE MONITOR                    │
│                                                  │
│  Datenquellen:          Funktionen:             │
│  ┌──────────────┐       ┌──────────────────┐   │
│  │ Metrics      │──────→│ Dashboards       │   │
│  │ Logs         │──────→│ Alerts           │   │
│  │ Traces       │──────→│ Autoscale        │   │
│  └──────────────┘       │ Workbooks        │   │
│                         │ Insights         │   │
│                         └──────────────────┘   │
│                                                  │
│  Log Analytics Workspace = Zentrale Datenbank   │
└─────────────────────────────────────────────────┘
```

**Metrics vs Logs:**
```
Metrics:
- Numerische Daten
- Zeitreihen (CPU %, RAM, etc.)
- Schnelle Abfragen
- 93 Tage Retention (Standard)

Logs:
- Detaillierte Events
- Text-basiert
- KQL (Kusto Query Language)
- Konfigurierbare Retention
```

### Azure Service Health

**Status von Azure selbst**

```
3 Bereiche:
─────────────────────────────────────
1. Azure Status:      Globale Ausfälle
                      → status.azure.com

2. Service Health:    Probleme die DICH betreffen
                      → Deine Regionen/Services

3. Resource Health:   Status deiner Ressourcen
                      → Ist meine VM gesund?

Alerts einrichten:
→ Service Health → Health Alerts → Create
→ Email bei Problemen in "West Europe"
```

### Azure Advisor

**Kostenlose Empfehlungen**

```
┌─────────────────────────────────────────────┐
│              AZURE ADVISOR                   │
│                                              │
│  Kategorien:                                │
│  ┌─────────────────────────────────────┐   │
│  │ 💰 Cost         "VM ist oversized"   │   │
│  │ 🔒 Security     "MFA nicht aktiv"    │   │
│  │ ⚡ Performance  "Disk zu langsam"    │   │
│  │ 🎯 Reliability  "Kein Backup"        │   │
│  │ ✨ Excellence   "Best Practices"     │   │
│  └─────────────────────────────────────┘   │
│                                              │
│  Score: 0-100% pro Kategorie                │
│  → Höher = besser                           │
└─────────────────────────────────────────────┘
```

### Application Insights

**Monitoring für deine Apps**

```python
# Python SDK Beispiel
from opencensus.ext.azure.trace_exporter import AzureExporter
from opencensus.trace.samplers import ProbabilitySampler
from opencensus.trace.tracer import Tracer

tracer = Tracer(
    exporter=AzureExporter(
        connection_string='InstrumentationKey=xxx'
    ),
    sampler=ProbabilitySampler(1.0)
)

with tracer.span(name='my_function'):
    # Dein Code hier
    pass
```

```
Was du siehst:
✓ Request-Zeiten
✓ Fehler-Rate
✓ Abhängigkeiten (DB, APIs)
✓ Custom Events
✓ User Flows
✓ Live Metrics
```

---

## Kapitel 10: Azure Security (Defense in Depth) ![AZ-900](https://learn.microsoft.com/en-us/media/learn/certification/badges/microsoft-certified-fundamentals-badge.svg)

### Defense in Depth

**Mehrere Sicherheitsebenen**

```
┌─────────────────────────────────────────────────────┐
│                    PHYSICAL                          │
│  (Datacenter: Zäune, Kameras, Biometrie)            │
│  ┌─────────────────────────────────────────────┐    │
│  │                  IDENTITY                    │    │
│  │  (Entra ID: MFA, Conditional Access)        │    │
│  │  ┌─────────────────────────────────────┐   │    │
│  │  │             PERIMETER                │   │    │
│  │  │  (DDoS, Firewall, WAF)              │   │    │
│  │  │  ┌─────────────────────────────┐   │   │    │
│  │  │  │          NETWORK             │   │   │    │
│  │  │  │  (NSG, VNet, Subnets)       │   │   │    │
│  │  │  │  ┌─────────────────────┐   │   │   │    │
│  │  │  │  │      COMPUTE         │   │   │   │    │
│  │  │  │  │  (VM Security)       │   │   │   │    │
│  │  │  │  │  ┌─────────────┐    │   │   │   │    │
│  │  │  │  │  │ APPLICATION │    │   │   │   │    │
│  │  │  │  │  │ ┌─────────┐│    │   │   │   │    │
│  │  │  │  │  │ │  DATA   ││    │   │   │   │    │
│  │  │  │  │  │ │(Encrypt)││    │   │   │   │    │
│  │  │  │  │  │ └─────────┘│    │   │   │   │    │
│  │  │  │  │  └─────────────┘    │   │   │   │    │
│  │  │  │  └─────────────────────┘   │   │   │    │
│  │  │  └─────────────────────────────┘   │   │    │
│  │  └─────────────────────────────────────┘   │    │
│  └─────────────────────────────────────────────┘    │
└─────────────────────────────────────────────────────┘
```

### Zero Trust Model

**"Never trust, always verify"**

```
Prinzipien:
──────────────────────────────────────
1. Verify explicitly
   → Immer authentifizieren + autorisieren
   → Alle Signale prüfen (User, Location, Device)

2. Least privilege access
   → Nur minimale Rechte geben
   → Just-In-Time (JIT) Access

3. Assume breach
   → Davon ausgehen, dass Angreifer drin sind
   → Micro-Segmentation
   → Encrypt everywhere
   → Analytics für Anomalien

Alt (Perimeter-basiert):    Neu (Zero Trust):
┌──────────────────┐        ┌──────────────────┐
│ 🏰 Firewall      │        │ Jeder Request:   │
│ Drinnen = Sicher │        │ - Wer bist du?   │
│ Draußen = Gefahr │        │ - Was darfst du? │
└──────────────────┘        │ - Ist das normal?│
                            └──────────────────┘
```

### Microsoft Defender for Cloud

**Security Posture Management + Threat Protection**

```
┌─────────────────────────────────────────────────┐
│          MICROSOFT DEFENDER FOR CLOUD            │
│                                                  │
│  Secure Score: 76/100                           │
│  ████████████████████░░░░░░                     │
│                                                  │
│  Empfehlungen:                                  │
│  ┌────────────────────────────────────────┐    │
│  │ ⚠️ MFA nicht für alle Admins aktiv      │    │
│  │ ⚠️ Storage Account erlaubt Public       │    │
│  │ ⚠️ SQL Firewall zu offen               │    │
│  │ ✅ VMs haben Updates installiert        │    │
│  └────────────────────────────────────────┘    │
│                                                  │
│  Threat Protection:                             │
│  → Alerts bei verdächtigem Verhalten           │
│  → Malware Detection                           │
│  → Brute Force Detection                       │
└─────────────────────────────────────────────────┘
```

### Azure Key Vault

**Sichere Aufbewahrung von Secrets**

```
Was speichern?
─────────────────────
- API Keys
- Passwörter
- Zertifikate
- Encryption Keys

Warum?
✓ Keine Secrets im Code
✓ Zentrale Verwaltung
✓ Access Policies
✓ Audit Logs
✓ HSM-backed (Hardware Security Module)

# Azure CLI
az keyvault create --name myVault --resource-group myRG

az keyvault secret set \
  --vault-name myVault \
  --name "OpenAI-Key" \
  --value "sk-xxx"

az keyvault secret show \
  --vault-name myVault \
  --name "OpenAI-Key"
```

### Network Security Groups (NSG)

**Firewall für VNets**

```
┌─────────────────────────────────────────────────┐
│                      NSG                         │
│                                                  │
│  Inbound Rules:         Outbound Rules:         │
│  ┌─────────────────┐   ┌─────────────────┐     │
│  │ Priority: 100   │   │ Priority: 100   │     │
│  │ Allow SSH (22)  │   │ Allow Internet  │     │
│  │ Source: My IP   │   │                 │     │
│  ├─────────────────┤   ├─────────────────┤     │
│  │ Priority: 200   │   │ Priority: 65000 │     │
│  │ Allow HTTPS     │   │ Deny All        │     │
│  │ Source: Any     │   │                 │     │
│  ├─────────────────┤   └─────────────────┘     │
│  │ Priority: 65500 │                           │
│  │ Deny All        │                           │
│  └─────────────────┘                           │
│                                                  │
│  → Niedrigere Priority = wird zuerst geprüft   │
└─────────────────────────────────────────────────┘
```

---

## Kapitel 11: Azure Networking (Erweitert) ![AZ-900](https://learn.microsoft.com/en-us/media/learn/certification/badges/microsoft-certified-fundamentals-badge.svg)

### Virtual Network (VNet) Deep Dive

```
┌─────────────────────────────────────────────────────┐
│              VNET: 10.0.0.0/16                       │
│                                                      │
│  ┌─────────────────┐    ┌─────────────────┐        │
│  │ Subnet: Web     │    │ Subnet: DB      │        │
│  │ 10.0.1.0/24     │    │ 10.0.2.0/24     │        │
│  │                 │    │                 │        │
│  │ ┌─────┐ ┌─────┐│    │ ┌─────┐        │        │
│  │ │ VM1 │ │ VM2 ││    │ │ SQL │        │        │
│  │ └─────┘ └─────┘│    │ └─────┘        │        │
│  │                 │    │                 │        │
│  │ NSG: Allow HTTP │    │ NSG: Only Web  │        │
│  └─────────────────┘    └─────────────────┘        │
│                                                      │
│  → Subnets können unterschiedliche NSGs haben       │
│  → Kommunikation zwischen Subnets standardmäßig OK  │
└─────────────────────────────────────────────────────┘
```

### VNet Peering

**VNets verbinden**

```
┌───────────────┐              ┌───────────────┐
│  VNet Europe  │◄────────────►│  VNet US      │
│  10.1.0.0/16  │   Peering    │  10.2.0.0/16  │
└───────────────┘              └───────────────┘

Eigenschaften:
✓ Traffic bleibt im Microsoft-Backbone
✓ Keine Gateways nötig
✓ Low Latency
✓ Auch zwischen Subscriptions möglich
✓ Auch zwischen Regionen (Global Peering)
```

### VPN Gateway

**Sichere Verbindung zu On-Premises**

```
┌─────────────────┐                    ┌─────────────────┐
│  On-Premises    │                    │  Azure VNet     │
│  192.168.0.0/16 │                    │  10.0.0.0/16    │
│                 │                    │                 │
│  ┌───────────┐  │   🔒 IPsec VPN    │  ┌───────────┐  │
│  │ VPN Device│◄─┼──────────────────►┼─►│VPN Gateway│  │
│  └───────────┘  │   (Internet)       │  └───────────┘  │
└─────────────────┘                    └─────────────────┘

Typen:
- Site-to-Site (S2S): Firma ↔ Azure
- Point-to-Site (P2S): Einzelner Laptop ↔ Azure
- VNet-to-VNet: Azure VNet ↔ Azure VNet
```

### ExpressRoute

**Private Verbindung zu Azure (nicht über Internet)**

```
┌─────────────────┐                    ┌─────────────────┐
│  On-Premises    │                    │  Azure          │
│                 │                    │                 │
│                 │   Private Leitung  │                 │
│                 │◄──────────────────►│                 │
│                 │   (kein Internet!) │                 │
└─────────────────┘                    └─────────────────┘
         ↑                                      ↑
         │                                      │
    Connectivity                          Microsoft
    Provider                              Edge Router
    (z.B. Telekom)

Vorteile:
✓ Höhere Bandbreite (bis 100 Gbps)
✓ Niedrigere Latenz
✓ Zuverlässiger als VPN
✓ Kein öffentliches Internet

Kosten: Ab ~200€/Monat + Provider-Kosten
```

### Azure Firewall

**Managed Cloud Firewall**

```
┌─────────────────────────────────────────────────────┐
│                   AZURE FIREWALL                     │
│                                                      │
│  Features:                                          │
│  ✓ Stateful Firewall                               │
│  ✓ Application Rules (FQDN-basiert)                │
│  ✓ Network Rules (IP-basiert)                      │
│  ✓ NAT Rules                                       │
│  ✓ Threat Intelligence                             │
│  ✓ TLS Inspection (Premium)                        │
│                                                      │
│  Beispiel-Regel:                                    │
│  "Allow *.github.com, *.docker.io"                 │
│  → Statt nur IP-Adressen                           │
│                                                      │
│  Kosten: ~900€/Monat + Traffic                     │
└─────────────────────────────────────────────────────┘
```

### Azure DDoS Protection

**Schutz vor Distributed Denial of Service**

```
Tiers:
──────────────────────────────────────
Basic (Kostenlos):
→ Automatisch für alle Azure-Ressourcen
→ Schutz gegen gängige Angriffe
→ Keine Konfiguration nötig

Standard (~3000€/Monat):
→ ML-basierte Erkennung
→ Angepasst an dein Traffic-Muster
→ Real-time Metrics
→ Alerting
→ Cost Protection (Erstattung bei Angriff)
```

### Azure Load Balancer

**Traffic verteilen**

```
                    ┌─────────────────┐
    Internet ─────► │  Load Balancer  │
                    └────────┬────────┘
                             │
              ┌──────────────┼──────────────┐
              ▼              ▼              ▼
         ┌────────┐    ┌────────┐    ┌────────┐
         │  VM 1  │    │  VM 2  │    │  VM 3  │
         └────────┘    └────────┘    └────────┘

Typen:
- Basic: Kostenlos, einfach
- Standard: Availability Zones, SLA 99.99%

Layer 4 (TCP/UDP) → Azure Load Balancer
Layer 7 (HTTP/S)  → Application Gateway
```

---

## Kapitel 12: Azure Solutions ![AZ-900](https://learn.microsoft.com/en-us/media/learn/certification/badges/microsoft-certified-fundamentals-badge.svg)

### Azure IoT Hub

**Internet of Things Platform**

```
┌─────────────────────────────────────────────────┐
│                  AZURE IoT HUB                   │
│                                                  │
│  ┌──────┐ ┌──────┐ ┌──────┐                    │
│  │Device│ │Device│ │Device│  ... Millionen     │
│  └──┬───┘ └──┬───┘ └──┬───┘                    │
│     │        │        │                         │
│     └────────┼────────┘                         │
│              ▼                                  │
│     ┌────────────────┐                         │
│     │    IoT Hub     │                         │
│     └───────┬────────┘                         │
│             │                                   │
│     ┌───────┴────────┐                         │
│     ▼                ▼                         │
│  Stream         Azure                          │
│  Analytics      Functions                      │
│     │                │                         │
│     ▼                ▼                         │
│  Storage       ML/Alerts                       │
└─────────────────────────────────────────────────┘

Use Cases:
→ Smart Home, Factory, City
→ Predictive Maintenance
→ Remote Monitoring
```

### Azure Synapse Analytics

**Big Data + Data Warehouse**

```
┌─────────────────────────────────────────────────┐
│              AZURE SYNAPSE ANALYTICS             │
│                                                  │
│  Datenquellen:                                  │
│  ┌─────────┐ ┌─────────┐ ┌─────────┐          │
│  │ SQL DB  │ │  Blob   │ │Cosmos DB│          │
│  └────┬────┘ └────┬────┘ └────┬────┘          │
│       │           │           │                │
│       └───────────┼───────────┘                │
│                   ▼                            │
│     ┌─────────────────────────────┐           │
│     │    Synapse Workspace        │           │
│     │  ┌────────┐  ┌────────┐    │           │
│     │  │Spark   │  │SQL Pool│    │           │
│     │  │Pools   │  │(DWH)   │    │           │
│     │  └────────┘  └────────┘    │           │
│     └─────────────────────────────┘           │
│                   │                            │
│                   ▼                            │
│            Power BI / ML                       │
└─────────────────────────────────────────────────┘
```

### Azure DevOps

**CI/CD + Projektmanagement**

```
Azure DevOps Services:
──────────────────────────────────────
1. Azure Repos     → Git Repositories
2. Azure Pipelines → CI/CD (Gratis für Open Source!)
3. Azure Boards    → Kanban, Sprints, Backlogs
4. Azure Artifacts → Package Management
5. Azure Test Plans→ Test Management

Alternative: GitHub + GitHub Actions
(Auch von Microsoft, oft einfacher)
```

### Azure Cognitive Services

**Fertige AI/ML APIs**

```
Vision:
- Computer Vision (Bild-Analyse)
- Face API (Gesichtserkennung)
- Custom Vision (Eigene Modelle)

Speech:
- Speech-to-Text
- Text-to-Speech
- Speech Translation

Language:
- Text Analytics (Sentiment)
- Translator
- LUIS (Language Understanding)
- Azure OpenAI Service (GPT-4, DALL-E)

Decision:
- Personalizer
- Content Moderator
- Anomaly Detector
```

---

## Kapitel 13: SLA, Support & Lifecycle ![AZ-900](https://learn.microsoft.com/en-us/media/learn/certification/badges/microsoft-certified-fundamentals-badge.svg)

### Service Level Agreements (SLA)

**Garantierte Verfügbarkeit**

```
Typische Azure SLAs:
──────────────────────────────────────
VMs (Single):           99.9%    (8.76h Downtime/Jahr)
VMs (Availability Set): 99.95%   (4.38h)
VMs (Availability Zone):99.99%   (52 min)

App Service:            99.95%
Azure SQL Database:     99.99%
Azure Functions:        99.95%
Storage (RA-GRS):       99.99%
Azure AD:               99.99%

Zusammengesetztes SLA:
App (99.95%) × DB (99.99%) = 99.94%
→ Mehr Komponenten = niedrigere Gesamt-SLA
```

### Was passiert bei SLA-Verletzung?

```
Service Credits (Gutschriften):
──────────────────────────────────────
< 99.99% aber ≥ 99%:     10% Credit
< 99% aber ≥ 95%:        25% Credit
< 95%:                   100% Credit

Beispiel:
→ VM-Rechnung: 100€/Monat
→ SLA 99.9% gebrochen (99.5%)
→ Erstattung: 25€

WICHTIG:
- Du musst Credit selbst beantragen!
- Innerhalb von 2 Monaten
- via Support Ticket
```

### Azure Support Plans

```
┌────────────────┬───────────────┬────────────────┬────────────────┐
│     BASIC      │   DEVELOPER   │   STANDARD     │  PROFESSIONAL  │
│   (Kostenlos)  │   (29$/mo)    │   (100$/mo)    │   (1000$/mo)   │
├────────────────┼───────────────┼────────────────┼────────────────┤
│ Docs, Forums   │ Email Support │ 24/7 Phone     │ 24/7 Phone     │
│ Billing Support│ Business Hours│ < 1h Critical  │ < 15min Crit.  │
│                │ < 8h Response │ < 4h High      │ < 2h High      │
│                │               │ Technical Acct │ + Proactive    │
│                │               │ Manager (TAM)  │ Guidance       │
└────────────────┴───────────────┴────────────────┴────────────────┘

Für Startups/Lernen: Basic oder Developer reicht
Für Production: Mindestens Standard
```

### Service Lifecycle

**Preview vs General Availability (GA)**

```
┌─────────────────────────────────────────────────────┐
│               SERVICE LIFECYCLE                      │
│                                                      │
│  1. Private Preview                                 │
│     → Nur eingeladene Kunden                        │
│     → Kein SLA, kein Support                        │
│                                                      │
│  2. Public Preview                                  │
│     → Jeder kann testen                             │
│     → Kein SLA, limitierter Support                 │
│     → Oft günstiger oder gratis                     │
│     → NICHT für Production!                         │
│                                                      │
│  3. General Availability (GA)                       │
│     → Production-ready                              │
│     → SLA garantiert                                │
│     → Voller Support                                │
│     → Normale Preise                                │
│                                                      │
│  4. Deprecation (Abkündigung)                       │
│     → 12 Monate Vorlauf (minimum)                   │
│     → Migration zu neuem Service                    │
└─────────────────────────────────────────────────────┘
```

---

## Kapitel 14: Azure Kosten-Tools ![AZ-900](https://learn.microsoft.com/en-us/media/learn/certification/badges/microsoft-certified-fundamentals-badge.svg)

### Azure Pricing Calculator

**Kosten VOR dem Deployen schätzen**

```
URL: azure.microsoft.com/pricing/calculator

So nutzen:
1. Produkte hinzufügen (z.B. VM, Storage)
2. Konfiguration wählen
3. Region wählen
4. Geschätzte Kosten sehen

Beispiel-Schätzung:
┌────────────────────────────────────────┐
│ D2s v3 VM (2 vCPU, 8 GB) West Europe  │
│ - Pay-as-you-go:        ~€65/mo       │
│ - 1 Year Reserved:      ~€40/mo       │
│ - 3 Year Reserved:      ~€26/mo       │
│                                        │
│ + 128 GB SSD:           ~€10/mo       │
│ + Outbound Traffic:     ~€5/mo        │
│ ────────────────────────────────      │
│ Total:                  ~€80/mo       │
└────────────────────────────────────────┘
```

### Total Cost of Ownership (TCO) Calculator

**Cloud vs On-Premises vergleichen**

```
URL: azure.microsoft.com/pricing/tco/calculator

Input:
┌────────────────────────────────────────┐
│ Aktuelle On-Premises Infrastruktur:   │
│ - 10 Server (Windows/Linux)           │
│ - 2 Datenbanken                       │
│ - 5 TB Storage                        │
│ - Strom, Kühlung, IT-Personal         │
└────────────────────────────────────────┘

Output:
┌────────────────────────────────────────┐
│ 5-Jahres-Vergleich:                   │
│                                        │
│ On-Premises:  €500,000                │
│ Azure:        €300,000                │
│ ─────────────────────                 │
│ Ersparnis:    €200,000 (40%)          │
│                                        │
│ Aufgeschlüsselt nach:                 │
│ - Hardware, Software, Datacenter      │
│ - IT-Personal, Strom                  │
│ - Netzwerk                            │
└────────────────────────────────────────┘
```

### Azure Cost Management

**Kosten NACH dem Deployen tracken**

```
Features:
─────────────────────────────────────
1. Cost Analysis
   → Wo geht das Geld hin?
   → Nach Resource Group, Tag, Service

2. Budgets
   → "Alert bei 80% von 500€"
   → Email-Benachrichtigungen

3. Recommendations
   → "Diese VM ist oversized"
   → "Reserved Instance würde 40% sparen"

4. Exports
   → Kosten-Daten als CSV
   → Für Buchhaltung/Reporting
```

### Kosten-Optimierung Strategien

```
1. Right-Sizing
   ─────────────────────────────────
   → VM-Größe an Bedarf anpassen
   → Azure Advisor Empfehlungen nutzen
   → Regelmäßig Auslastung prüfen

2. Reserved Instances
   ─────────────────────────────────
   → 1 Jahr: ~40% sparen
   → 3 Jahre: ~60% sparen
   → Nur für stabile Workloads!

3. Spot VMs
   ─────────────────────────────────
   → Ungenutzte Kapazität
   → Bis zu 90% günstiger
   → Kann jederzeit gestoppt werden
   → Gut für: Batch Jobs, Dev/Test

4. Auto-Shutdown
   ─────────────────────────────────
   → Dev-VMs nachts ausschalten
   → ~70% Kosten sparen
   → Azure Auto-Shutdown Feature

5. Tags für Kostenzuordnung
   ─────────────────────────────────
   → project: xyz
   → environment: dev/prod
   → costcenter: abc
   → Filtern nach Tags in Cost Analysis

6. Azure Hybrid Benefit
   ─────────────────────────────────
   → Windows Server Lizenzen mitbringen
   → Bis zu 40% sparen
   → Auch für SQL Server
```

---

# TEIL 2: PRAKTISCHE UMSETZUNG

---

## Kapitel 15: Provider Empfehlungen

### Für AI-Projekte

| Provider | Wofür? | Kosten | Für wen? |
|----------|--------|--------|----------|
| **Hetzner** | CPU VMs, super günstig | 5-50€/mo | Budget, EU-Hosting |
| **DigitalOcean** | Easy VMs, gute Docs | 10-50€/mo | Anfänger |
| **Railway** | PaaS, Git-Deploy | 0-50€/mo | Schnelles Prototyping |
| **Render** | PaaS, Free Tier | 0-50€/mo | Side Projects |
| **Azure** | Enterprise, Azure OpenAI | 20-500€/mo | Wenn Azure OpenAI gebraucht |
| **AWS** | Alles, komplex | 20-1000€/mo | Enterprise |
| **RunPod** | GPU VMs | 0.5-5$/h | Model Training/Inference |
| **Lambda Labs** | GPU VMs | 1-10$/h | ML Research |

### Meine Empfehlung für GenZ-Projekte

```
Phase 1 - MVP/Prototyp:
→ Railway oder Render (Free Tier)
→ Hetzner wenn mehr Kontrolle
→ Kosten: 0-20€/Monat

Phase 2 - Erste User:
→ Hetzner Cloud (CX21 oder CX31)
→ Kosten: 10-30€/Monat

Phase 3 - Wachstum:
→ DigitalOcean oder Azure
→ Kosten: 50-200€/Monat

Für Azure-Erfahrung (AZ-900):
→ Azure Free Account (200$ Guthaben)
→ Azure for Students (100$ Guthaben)
```

---

## Kapitel 16: Server Setup (Hetzner Beispiel)

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

## Kapitel 17: Docker

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

## Kapitel 18: Deployment

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

## Kapitel 19: HTTPS & Domain

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

## Kapitel 20: Monitoring (Praktisch)

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

## Kapitel 21: Kosten-Tracking (Praktisch)

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

## Kapitel 22: Security Checklist

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

## Kapitel 23: Troubleshooting

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

### Für AZ-900 Zertifizierung:
1. **Cloud-Basics**: Kapitel 1-6 (IaaS/PaaS/SaaS, CapEx/OpEx, HA, Skalierung)
2. **Azure-Spezifisch**: Kapitel 6-14 (Services, Governance, Security, Networking)
3. **Praxis üben**: Azure Free Account erstellen, Portal erkunden
4. **Mock Exams**: Microsoft Learn Practice Tests

### Für dein AI-Projekt:
1. **Provider wählen**: Kapitel 15 (Hetzner/Railway für Start)
2. **Server aufsetzen**: Kapitel 16-19 (Setup, Docker, Deploy, HTTPS)
3. **Monitoring**: Kapitel 20 (Logs, Health Checks)
4. **Security**: Kapitel 22 Checklist durchgehen

### AZ-900 Prüfungs-Tipps:
```
Prüfungsformat:
- 40-60 Fragen
- 60 Minuten Zeit
- 700/1000 Punkte zum Bestehen
- ~€100 Prüfungsgebühr

Themengewichtung:
- Cloud Concepts: 25-30%
- Azure Architecture: 35-40%
- Management & Governance: 30-35%

Lernressourcen:
→ Microsoft Learn (kostenlos!)
→ Dieses Playbook 😉
→ Azure Free Account zum Üben
```

Du hast das. Ship it! 🚀
