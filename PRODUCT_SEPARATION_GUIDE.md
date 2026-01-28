# Produktseparation - Guide för Multi-Repo Struktur

**Syfte:** Skapa ett duplicerbart system där varje produkt har sitt eget repo, med delad infrastruktur i spitakolus.

---

## ⚠️ Nuvarande Problem

### Duplicerat Flocken-innehåll

**nastahem repo** innehåller fortfarande Flocken-filer som borde vara i flocken-website:

```
nastahem/
├── src/app/flocken/              ❌ Borde tas bort
│   ├── page.tsx
│   ├── anvandarvillkor/
│   └── components/
├── public/assets/flocken/        ❌ Borde tas bort
│   ├── generated/
│   ├── logo/
│   └── screenshots/
└── docs/flocken/                 ⚠️ Flytta till flocken-website
    ├── brand/
    │   ├── personas/
    │   ├── color_system.md
    │   ├── tone_of_voice.md
    │   └── visual_style.md
    └── marketing/
```

**flocken-website repo** har sin egen version:

```
flocken-website/
├── app/                          ✅ Korrekt
├── public/assets/flocken/        ✅ Korrekt
└── docs/                         ⚠️ Saknar brand/personas
```

---

## 🎯 Målstruktur

### Princip: Varje produkt = Ett repo

```
C:\Dev\
├── spitakolus/                   # Delad dokumentation
│   ├── tracking/                 # Delad tracking-infrastruktur
│   ├── meta-ads/                 # Delade Meta Ads standarder
│   ├── development/              # Delade utvecklingsstandarder
│   │   └── TEMPLATES/            # Mallar för nya produkter
│   └── PRODUCT_SEPARATION_GUIDE.md
│
├── nastahem/                     # Nästa Hem produkt
│   ├── src/app/                  # Endast Nästa Hem sidor
│   ├── public/assets/nastahem/   # Endast Nästa Hem assets
│   ├── docs/                     # Nästa Hem-specifik dokumentation
│   │   ├── brand/                # Nästa Hem brand
│   │   └── tracking/             # Nästa Hem-specifik tracking
│   └── README.md                 # Tydlig varning om repo-identitet
│
├── flocken-website/              # Flocken produkt
│   ├── app/                      # Endast Flocken sidor
│   ├── public/assets/flocken/    # Endast Flocken assets
│   ├── docs/                     # Flocken-specifik dokumentation
│   │   ├── brand/                # Flocken brand (flyttas från nastahem)
│   │   └── tracking/             # Flocken-specifik tracking
│   └── README.md                 # Tydlig varning om repo-identitet
│
└── [framtida-produkt]/           # Ny produkt (samma struktur)
    ├── app/
    ├── public/assets/[produkt]/
    └── docs/
```

---

## ✅ Åtgärder att utföra

### 1. Flytta Flocken brand-dokumentation från nastahem till flocken-website

**Filer att flytta:**
```
nastahem/docs/flocken/brand/ → flocken-website/docs/brand/
  ├── personas/
  │   ├── anders_rasta_explorer_01.md
  │   ├── anna_passa_safety_01.md
  │   ├── jonas_allround_community_01.md
  │   ├── marco_para_researcher_01.md
  │   └── README.md
  ├── color_system.md
  ├── tone_of_voice.md
  ├── value_proposition.md
  └── visual_style.md

nastahem/docs/flocken/marketing/ → flocken-website/docs/marketing/
  └── LAUNCH_PLAN.md
```

### 2. Ta bort Flocken-kod från nastahem

**Filer/mappar att ta bort från nastahem:**
```
nastahem/src/app/flocken/         # Hela mappen
nastahem/public/assets/flocken/   # Hela mappen
nastahem/docs/flocken/            # Hela mappen (efter flytt)
```

### 3. Uppdatera nastahem README.md

Lägg till tydlig varning:
```markdown
**⚠️ VIKTIGT:** Detta är **NASTAHEM** repo.
- För Flocken-projektet, se [flocken-website](https://github.com/tbinho/flocken-website)
- För delad dokumentation, se [spitakolus](https://github.com/tbinho/spitakolus)
```

### 4. Verifiera flocken.info fungerar

Alla länkar på flocken.info använder `/assets/flocken/`:
- ✅ `/assets/flocken/generated/hero.png`
- ✅ `/assets/flocken/screenshots/flocken_*.png`
- ✅ `/assets/flocken/videos/*.mp4`

Dessa finns i flocken-website/public/assets/flocken/ ✅

---

## 📋 Duplicerbar struktur för ny produkt

### Steg-för-steg guide för att lägga till ny produkt

**1. Skapa nytt repo:**
```bash
# GitHub: Skapa repo [produkt-namn]
# Lokalt:
cd C:\Dev
git clone https://github.com/tbinho/[produkt-namn].git
```

**2. Skapa grundstruktur:**
```
[produkt-namn]/
├── app/                          # Next.js App Router
├── components/                   # Komponenter
├── lib/                          # Utilities
├── public/
│   └── assets/
│       └── [produkt]/            # Produktens assets
│           ├── _originals/       # Originalbilder
│           ├── generated/        # Processade bilder
│           ├── logo/             # Logotyper
│           ├── screenshots/      # Screenshots
│           └── videos/           # Videos
├── docs/
│   ├── brand/                    # Brand guidelines
│   │   └── personas/             # Personas
│   ├── tracking/                 # Produktspecifik tracking
│   └── README.md                 # Dokumentationsindex
├── README.md                     # ⚠️ Med tydlig varning
└── DOCUMENTATION_MAP.md          # Komplett dokumentationskarta
```

**3. Skapa README.md med varning:**
```markdown
# [Produkt-namn]

**⚠️ VIKTIGT:** Detta är **[PRODUKT-NAMN]** repo.
- För andra projekt, se respektive repo
- För delad dokumentation, se [spitakolus](https://github.com/tbinho/spitakolus)

## Deploy
- **URL:** [produkt].com
- **Vercel:** [produkt-namn] projekt
```

**4. Skapa DOCUMENTATION_MAP.md:**
Använd mall från `spitakolus/development/TEMPLATES/DOCUMENTATION_MAP_TEMPLATE.md`

**5. Konfigurera delad infrastruktur:**
- GTM: Lägg till hostname routing (se `spitakolus/tracking/GTM_SHARED_CONTAINER.md`)
- BigQuery: Skapa datasets `[produkt]_raw`, `[produkt]_curated`, `[produkt]_marts`
- GA4: Skapa property för produkten

---

## 🔗 Länkar mellan repos

### Varje produkt-repo ska ha:

1. **README.md** med:
   - Tydlig varning om vilket repo det är
   - Länk till spitakolus för delad dokumentation
   - Länk till andra produkt-repos

2. **DOCUMENTATION_MAP.md** med:
   - Komplett karta över lokal dokumentation
   - Länkar till delad dokumentation i spitakolus

3. **docs/tracking/SHARED_INFRASTRUCTURE.md** med:
   - Översikt över delad infrastruktur
   - Länkar till spitakolus för detaljer

---

## 📊 Asset-struktur per produkt

```
public/assets/[produkt]/
├── _originals/                   # Originalfiler (ej versionshanterade)
│   └── [bild].png
├── generated/                    # Processade/optimerade bilder
│   └── [bild].[avif|webp|jpg]
├── logo/                         # Logotyper
│   ├── logo_icon_[produkt]_large_1x1.png
│   └── logo_icon_[produkt]_small_1x1.png
├── screenshots/                  # App screenshots
│   └── [produkt]_[funktion]_[beskrivning].png
└── videos/                       # Videos
    └── [produkt]_[funktion].mp4
```

### Naming convention:
- Prefix med produktnamn: `flocken_`, `nastahem_`
- Beskrivande namn: `flocken_para_karta-alla-hundar.png`
- Konsistent format: snake_case

---

**Senast uppdaterad:** 2026-01-28
