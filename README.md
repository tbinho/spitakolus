# Spitakolus - Delad Företagsdokumentation

**⚠️ VIKTIGT:** Detta är **SPITAKOLUS** repo - delad dokumentation för alla produkter.  
Detta repo innehåller INTE produktkod - varje produkt har sitt eget repo.

**🤖 AI-assistenter:** Läs [AI_ONBOARDING.md](./AI_ONBOARDING.md) för snabb insättning!

---

## 🏢 Spitakolus-produkter

| Produkt | Beskrivning | Repo | URL |
|---------|-------------|------|-----|
| **🏠 Nästa Hem** | AI-driven fastighetsmäklarplattform | [nastahem](https://github.com/tbinho/nastahem) | nastahem.com |
| **🐕 Flocken** | Hundägare community & app | [flocken-website](https://github.com/tbinho/flocken-website) | flocken.info |

---

## 📁 Vad finns här?

### Delad infrastruktur och standarder

```
spitakolus/
├── tracking/                     # Delad tracking-infrastruktur
│   ├── GTM_SHARED_CONTAINER.md   # GTM container (GTM-PD5N4GT3)
│   ├── BIGQUERY_SHARED_PROJECT.md # BigQuery (nastahem-tracking)
│   ├── GOOGLE_ANALYTICS_EVALUATION.md
│   └── GA4_PROPERTY_STRUCTURE.md
│
├── meta-ads/                     # Delade Meta Ads standarder
│   ├── NAMING_CONVENTIONS.md     # Naming conventions (cid, etc.)
│   └── CREATIVE_WORKFLOW.md      # Creative Bases workflow
│
├── development/                  # Delade utvecklingsstandarder
│   ├── TEMPLATES/                # Mallar för nya produkter
│   │   ├── README_TEMPLATE.md
│   │   └── DOCUMENTATION_MAP_TEMPLATE.md
│   ├── GIT_WORKFLOW.md
│   ├── ASSET_STRUCTURE_STANDARD.md  # Standard för bilder/assets
│   └── IMAGE_PROCESSING_SYSTEM.md   # Bildhanteringssystem
│
├── company/                      # Företagsinformation
│   ├── COMPANY_INFO.md
│   └── CONTACT.md
│
├── skills/                       # Claude Skills för AI-assistenter
│   ├── spitakolus-navigation/    # Repo-navigation + Growth Loop vision
│   ├── spitakolus-documentation/ # Dokumentationsregler
│   └── spitakolus-tracking/      # GTM, GA4, BigQuery setup
│
├── DOCUMENTATION_RULES.md        # Regler för dokumentation
└── PRODUCT_SEPARATION_GUIDE.md   # Guide för multi-repo struktur
```

---

## 🎯 Användning

### För tracking och analytics
1. Varje produkt har sin egen GA4 property
2. Alla produkter delar GTM container (GTM-PD5N4GT3) med hostname-routing
3. Alla produkter delar BigQuery projekt (nastahem-tracking) med separata datasets

**Se:** [tracking/GTM_SHARED_CONTAINER.md](./tracking/GTM_SHARED_CONTAINER.md)

### För Meta Ads
1. Varje produkt har sina egna kampanjer
2. Alla produkter följer samma naming conventions
3. Creative workflow är delad

**Se:** [meta-ads/NAMING_CONVENTIONS.md](./meta-ads/NAMING_CONVENTIONS.md)

### För ny produkt
1. Skapa nytt repo för produkten
2. Använd mallar från `development/TEMPLATES/`
3. Lägg till hostname routing i GTM
4. Skapa BigQuery datasets

**Se:** [PRODUCT_SEPARATION_GUIDE.md](./PRODUCT_SEPARATION_GUIDE.md)

---

## ⚠️ AI-varningar

### ❌ UNDVIK FÖRVIRRING

**Detta repo (spitakolus) innehåller:**
- Delad dokumentation
- Standarder och mallar
- Infrastruktur-dokumentation

**Detta repo innehåller INTE:**
- Produktkod
- Produktspecifik dokumentation
- Assets eller bilder

### 🔗 Rätt repo för rätt uppgift

| Uppgift | Repo |
|---------|------|
| Arbeta med Nästa Hem webbplats | [nastahem](https://github.com/tbinho/nastahem) |
| Arbeta med Flocken webbplats | [flocken-website](https://github.com/tbinho/flocken-website) |
| Läsa/uppdatera delade standarder | **spitakolus** (detta repo) |

---

## 📊 Delad infrastruktur

### GTM Shared Container
- **Web Container:** GTM-PD5N4GT3
- **Server Container:** GTM-THB49L3K @ gtm.nastahem.com
- **Routing:** Hostname-based (nastahem.com, flocken.info)

### BigQuery Shared Project
- **Project:** nastahem-tracking
- **Nästa Hem datasets:** nastahem_raw, nastahem_curated, nastahem_marts
- **Flocken datasets:** flocken_raw, flocken_curated, flocken_marts

---

**Senast uppdaterad:** 2026-01-28
