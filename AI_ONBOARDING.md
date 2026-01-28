# AI Onboarding - Snabb Insättning för Claude/AI

**Detta dokument ger AI-assistenter snabb kontext för att arbeta med Spitakolus-projekt.**

---

## 🏢 Spitakolus AB

**Vad:** Tech-bolag med två jämbördiga produkter  
**Org.nr:** 559554-6101  
**Kontakt:** support@spitakolus.com

---

## 📦 Produkter och Repos

| Produkt | Repo | URL | Deployment |
|---------|------|-----|------------|
| 🐕 **Flocken** | [flocken-website](https://github.com/tbinho/flocken-website) | flocken.info | `git push raquel main` |
| 🏠 **Nästa Hem** | [nastahem](https://github.com/RaquelSandblad/nastahem) | nastahem.com | `git commit --author="RaquelSandblad <raquel.sandblad@hotmail.com>"` |
| 📚 **Spitakolus** | [spitakolus](https://github.com/tbinho/spitakolus) | (docs only) | `git push origin main` |

---

## ⚠️ KRITISKA REGLER

### 1. Kontrollera ALLTID vilket repo du är i
```markdown
- flocken-website → flocken.info
- nastahem → nastahem.com
- spitakolus → delad dokumentation
```

### 2. Läs DOCUMENTATION_MAP.md först
Varje projekt-repo har en `DOCUMENTATION_MAP.md` med komplett översikt.

### 3. Deployment kräver specifik remote/author
- **Flocken:** `git push raquel main` (inte origin!)
- **Nästa Hem:** `git commit --author="RaquelSandblad <raquel.sandblad@hotmail.com>"`

### 4. Delad vs Projekt-specifik dokumentation
- **Delad:** spitakolus repo (tracking, meta-ads, standarder)
- **Projekt-specifik:** respektive projekt-repo

---

## 🗂️ Dokumentationsstruktur

### I varje projekt-repo:
```
[projekt]/
├── README.md                 # Start här - med varning om vilket repo
├── DOCUMENTATION_MAP.md      # Komplett översikt
├── docs/
│   ├── tracking/             # Tracking-dokumentation
│   ├── meta/                 # Meta Ads-dokumentation
│   ├── bigquery/             # BigQuery-dokumentation
│   └── development/          # Utvecklingsdokumentation
└── [kod...]
```

### I spitakolus (delad):
```
spitakolus/
├── tracking/                 # Delad tracking (GTM, BigQuery)
├── meta-ads/                 # Delade naming conventions
├── development/              # Utvecklingsstandarder + mallar
├── company/                  # Företagsinfo
├── DOCUMENTATION_RULES.md    # Hur man dokumenterar
└── PRODUCT_SEPARATION_GUIDE.md  # Multi-repo guide
```

---

## 🔧 Tech Stack

**Båda produkterna:**
- Next.js 15+ (App Router)
- TypeScript
- Tailwind CSS
- Vercel deployment

**Nästa Hem specifikt:**
- Supabase
- MailerSend
- BigQuery

**Flocken specifikt:**
- Cookie consent (GDPR)
- Meta Pixel

---

## 📊 Delad Infrastruktur

### GTM (Google Tag Manager)
- **Web Container:** GTM-PD5N4GT3 (delad)
- **Server Container:** GTM-THB49L3K @ gtm.nastahem.com
- **Routing:** Hostname-based (nastahem.com, flocken.info)

### BigQuery
- **Project:** nastahem-tracking
- **Nästa Hem:** nastahem_raw, nastahem_curated, nastahem_marts
- **Flocken:** flocken_raw, flocken_curated, flocken_marts

### GA4
- **Nästa Hem:** G-7N67P0KT0B
- **Flocken:** G-7B1SVKL89Q

---

## 🚀 Quick Start per Projekt

### Flocken (flocken-website)
```bash
cd C:\Dev\flocken-website
npm install
npm run dev
# Deployment: git push raquel main
```

**Läs:** [DOCUMENTATION_MAP.md](https://github.com/tbinho/flocken-website/blob/main/DOCUMENTATION_MAP.md)

### Nästa Hem (nastahem)
```bash
cd C:\Dev\nastahem
npm install
npm run dev
# Deployment: git commit --author="RaquelSandblad <raquel.sandblad@hotmail.com>" -m "msg"
```

**Läs:** [DOCUMENTATION_MAP.md](https://github.com/tbinho/nastahem/blob/main/DOCUMENTATION_MAP.md)

---

## 📋 Vanliga Uppgifter

### Uppdatera webbplats
1. Identifiera rätt repo
2. Gör ändringar
3. Använd rätt deployment-metod

### Lägga till tracking
1. Läs [spitakolus/tracking/GTM_SHARED_CONTAINER.md](./tracking/GTM_SHARED_CONTAINER.md)
2. Lägg till tag med hostname condition
3. Testa i GTM Preview mode

### Lägga till bilder
1. Läs [spitakolus/development/IMAGE_PROCESSING_SYSTEM.md](./development/IMAGE_PROCESSING_SYSTEM.md)
2. Lägg i `_originals/`
3. Kör `node scripts/image-processor-[produkt].js process-all`

### Skapa Meta Ads
1. Läs [spitakolus/meta-ads/NAMING_CONVENTIONS.md](./meta-ads/NAMING_CONVENTIONS.md)
2. Följ cid-strukturen
3. Använd Creative Bases workflow

---

## ❌ Vanliga Misstag

| Misstag | Konsekvens | Lösning |
|---------|------------|---------|
| Pusha till fel remote | Deployment triggas inte | Använd rätt remote/author |
| Arbeta i fel repo | Kod hamnar på fel plats | Kontrollera alltid repo först |
| Skapa delad doc i projekt-repo | Duplicering | Lägg i spitakolus |
| Glömma image processor | Bilder inte optimerade | Kör `process-all` |

---

## 🔗 Viktiga Länkar

**Repos:**
- https://github.com/tbinho/flocken-website
- https://github.com/RaquelSandblad/nastahem
- https://github.com/tbinho/spitakolus

**Produktion:**
- https://flocken.info
- https://nastahem.com

**Tools:**
- GTM: https://tagmanager.google.com
- GA4: https://analytics.google.com
- BigQuery: https://console.cloud.google.com/bigquery

---

**Senast uppdaterad:** 2026-01-28
