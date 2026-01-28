# Organisation Plan - Delad vs Projekt-specifik Dokumentation

**Datum:** 2026-01-28  
**Status:** Planering

---

## 🎯 Analys: Vad är delat vs projekt-specifikt?

### ✅ DELAT (ska till spitakolus)

#### 1. GTM Shared Container
**Delat:**
- Container ID: `GTM-PD5N4GT3` (används av både Flocken och Nästa Hem)
- Server Container: `GTM-THB49L3K` @ `gtm.nastahem.com` (delas)
- Hostname routing koncept (delas mellan projekt)
- Consent Mode v2 setup (delas)

**Projekt-specifikt (stannar i flocken-website):**
- Flocken GA4 Measurement ID: `G-7B1SVKL89Q`
- Flocken-specifik trigger: `Page Hostname equals flocken.info`
- Flocken-specifik tag-konfiguration

#### 2. BigQuery Shared Project
**Delat:**
- Project ID: `nastahem-tracking` (används av både Flocken och Nästa Hem)
- Location: EU (europe-west1) (delas)
- Projekt-struktur och best practices (delas)

**Projekt-specifikt (stannar i flocken-website):**
- Flocken datasets: `flocken_raw`, `flocken_curated`, `flocken_marts`
- Flocken-specifika views och queries
- Flocken GA4 Property ID: `518338757`

#### 3. Meta Ads Naming Conventions
**Delat:**
- Grundprinciper (tecken, format, regler)
- CID-logik (primärnyckel-system)
- Campaign/Ad Set/Ad format-struktur
- Best practices för analys

**Projekt-specifikt (stannar i flocken-website):**
- Flocken-specifik vokabulär (`flo`, `dogowner`, `sitter`, etc.)
- Flocken-specifika campaigns och creative bases
- Flocken-specifik Meta Ads struktur (`meta_ads_structure_flocken.md`)

---

## 📋 Plan: Vad ska flyttas/kopieras

### Steg 1: Skapa delad dokumentation i spitakolus

#### 1.1 GTM_SHARED_CONTAINER.md
**Innehåll:**
- Container ID: GTM-PD5N4GT3
- Server Container: GTM-THB49L3K @ gtm.nastahem.com
- Hostname routing koncept och best practices
- Hur man lägger till nytt projekt i shared container
- Consent Mode v2 setup

**Källa:** Extraheras från:
- `flocken-website/docs/tracking/GTM_SETUP_INSTRUCTIONS.md`
- `flocken-website/docs/tracking/TRACKING_SETUP_COMPLETE.md`

#### 1.2 BIGQUERY_SHARED_PROJECT.md
**Innehåll:**
- Project ID: nastahem-tracking
- Location: EU (europe-west1)
- Projekt-struktur och best practices
- Hur man skapar datasets för nytt projekt
- Service account setup

**Källa:** Extraheras från:
- `flocken-website/docs/bigquery/BIGQUERY_SETUP_INSTRUCTIONS.md`
- `flocken-website/docs/bigquery/BIGQUERY_CLEAN_SETUP_EU.md`

#### 1.3 NAMING_CONVENTIONS.md (Meta Ads)
**Innehåll:**
- Grundprinciper (tecken, format, regler)
- CID-logik (primärnyckel-system)
- Campaign/Ad Set/Ad format-struktur
- Best practices för analys
- Exempel (generiska, inte projekt-specifika)

**Källa:** Extraheras från:
- `flocken-website/meta_ads_structure_flocken.md` (endast delad del)

#### 1.4 CREATIVE_WORKFLOW.md (Meta Ads)
**Innehåll:**
- Creative Bases koncept
- Brief-struktur
- Copy-struktur
- Variant-hantering
- Asset-hantering

**Källa:** Extraheras från:
- `flocken-website/creative_structure_flocken.md` (endast delad del)

---

### Steg 2: Uppdatera flocken-website dokumentation

#### 2.1 Uppdatera GTM-dokumentation
**Ändringar:**
- Ta bort delad information om GTM container
- Lägg till länkar till `spitakolus/tracking/GTM_SHARED_CONTAINER.md`
- Behåll Flocken-specifik information (G-7B1SVKL89Q, flocken.info)

**Filer att uppdatera:**
- `docs/tracking/GTM_SETUP_INSTRUCTIONS.md`
- `docs/tracking/TRACKING_SETUP_COMPLETE.md`
- `docs/tracking/GA4_SETUP_STATUS.md`

#### 2.2 Uppdatera BigQuery-dokumentation
**Ändringar:**
- Ta bort delad information om BigQuery projekt
- Lägg till länkar till `spitakolus/tracking/BIGQUERY_SHARED_PROJECT.md`
- Behåll Flocken-specifik information (flocken_raw, flocken_curated, flocken_marts)

**Filer att uppdatera:**
- `docs/bigquery/BIGQUERY_SETUP_INSTRUCTIONS.md`
- `docs/bigquery/BIGQUERY_CLEAN_SETUP_EU.md`
- Alla BigQuery-dokument som nämner nastahem-tracking

#### 2.3 Uppdatera Meta Ads-dokumentation
**Ändringar:**
- Lägg till länkar till `spitakolus/meta-ads/NAMING_CONVENTIONS.md`
- Lägg till länkar till `spitakolus/meta-ads/CREATIVE_WORKFLOW.md`
- Behåll Flocken-specifik struktur (`meta_ads_structure_flocken.md`)

**Filer att uppdatera:**
- `meta_ads_structure_flocken.md` (lägg till referens till delad naming conventions)
- `creative_structure_flocken.md` (lägg till referens till delad workflow)
- `docs/meta/META_ADS_COMPLETE_GUIDE.md`

---

### Steg 3: Skapa sammanfattningsdokument

#### 3.1 I flocken-website
**Skapa:** `docs/tracking/SHARED_INFRASTRUCTURE.md`
- Sammanfattning av delad infrastruktur
- Länkar till spitakolus för detaljerad info
- Flocken-specifik information

#### 3.2 I spitakolus
**Uppdatera:** `tracking/README.md`
- Komplett översikt över delad tracking-infrastruktur
- Länkar till projekt-specifik dokumentation

---

## ✅ Checklista

### Delad dokumentation (spitakolus)
- [ ] GTM_SHARED_CONTAINER.md - Komplett med delad info
- [ ] BIGQUERY_SHARED_PROJECT.md - Komplett med delad info
- [ ] SHARED_EVENTS_CONVENTIONS.md - Event naming (om delas)
- [ ] NAMING_CONVENTIONS.md - Meta Ads naming (delad del)
- [ ] CREATIVE_WORKFLOW.md - Meta Ads creative workflow (delad del)
- [ ] ACCOUNT_STRUCTURE.md - Meta Ads kontostruktur (om delas)

### Projekt-specifik dokumentation (flocken-website)
- [ ] Behåll Flocken-specifik GTM setup
- [ ] Behåll Flocken-specifika BigQuery datasets
- [ ] Behåll Flocken-specifik Meta Ads struktur
- [ ] Lägg till länkar till spitakolus för delad info
- [ ] Uppdatera alla referenser

### Länkar och referenser
- [ ] Uppdatera DOCUMENTATION_MAP.md med länkar till spitakolus
- [ ] Uppdatera docs/README.md med länkar till spitakolus
- [ ] Uppdatera README.md med länkar till spitakolus
- [ ] Verifiera att alla länkar fungerar

---

## 🎯 Resultat

Efter organisation:
- ✅ Delad dokumentation finns i spitakolus
- ✅ Projekt-specifik dokumentation finns i flocken-website
- ✅ Tydliga länkar mellan repos
- ✅ Inga dupliceringar av delad information
- ✅ Konsistent struktur över alla repos

---

**Senast uppdaterad:** 2026-01-28
