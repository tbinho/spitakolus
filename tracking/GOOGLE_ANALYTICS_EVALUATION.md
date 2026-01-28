# Google Analytics Setup - Utvärdering & Best Practices

**Datum:** 2025-01-03  
**Syfte:** Utvärdera och dokumentera best practices för Google Analytics setup  
**Status:** ✅ Utvärdering klar, best practices dokumenterade

**⚠️ VIKTIGT:** Detta är delad dokumentation. För projekt-specifik implementation, se projekt-repos.

---

## 📊 Utvärdering: Nästa Hems Setup

### ✅ **Mycket bra uppsättning - Professionell arkitektur**

Nästa Hems Google Analytics setup är **enterprise-grade** och följer best practices:

#### **Arkitektur:**

```
Next.js App (nastahem.com)
    ↓ (dataLayer.push)
GTM Web Container (GTM-PD5N4GT3)  
    ↓ (server-side routing)
GTM Server Container (GTM-THB49L3K) @ gtm.nastahem.com
    ↓ (measurement protocol)
GA4 Property (G-7N67P0KT0B)
    ↓ (daily + streaming export)
BigQuery Raw Data (nastahem-tracking.nastahem_raw)
    ↓ (SQL transformations)
Curated Analytics (nastahem_curated)
    ↓ (business intelligence)
Dashboard-Ready Marts (nastahem_marts)
```

#### **Fördelar med denna setup:**

1. **✅ Server-side tracking**
   - Bättre data quality (server-side validering)
   - Privacy-first (bättre consent handling)
   - Future-proof (redo för cookieless tracking)
   - Bättre prestanda (mindre client-side load)

2. **✅ GTM-only implementation**
   - Inga konflikter (ingen gtag.js direkt)
   - Centraliserad tag management
   - Enkel att underhålla och uppdatera

3. **✅ BigQuery integration**
   - Data warehouse för långsiktig analys
   - SQL-baserad data processing
   - Business intelligence ready
   - Google Ads optimization data

4. **✅ Cookie consent integration**
   - Consent Mode v2
   - GDPR-compliant
   - Privacy-first approach

5. **✅ Cross-platform ready**
   - Identity stitching för framtida app integration
   - Unified analytics för web + app

#### **Tekniska detaljer:**

**GTM Web Container (GTM-PD5N4GT3):**
- Client-side tag management
- Consent Mode v2 konfiguration
- Event tracking via dataLayer

**GTM Server Container (GTM-THB49L3K):**
- Server-side på `gtm.nastahem.com`
- Enhanced data quality
- Better privacy compliance

**GA4 Property (G-7N67P0KT0B):**
- Standard GA4 tracking
- BigQuery export (daily + streaming)
- Google Ads integration ready

**BigQuery Pipeline:**
- Raw → Curated → Marts
- Automated daily processing
- Business intelligence queries

---

## 🎯 Rekommendation: Använd samma setup för alla projekt

### **Varför samma setup?**

1. **✅ Beprövad metod** - Fungerar i produktion
2. **✅ Professionell arkitektur** - Enterprise-grade tracking
3. **✅ Skalbar** - Redo för framtida app integration
4. **✅ Privacy-first** - GDPR-compliant med Consent Mode v2
5. **✅ Data quality** - Server-side tracking ger bättre data

### **Anpassningar per projekt:**

1. **Separata GA4 Properties** - Varje projekt behöver egen GA4 property
2. **Separata BigQuery datasets** - `[projekt]_raw`, `[projekt]_curated`, `[projekt]_marts`
3. **GTM routing** - Samma GTM containers men med hostname-routing
4. **Projekt-specifika conversion values** - Varje projekt har egna värden

---

## 🚀 Implementation Plan för nytt projekt

### **Fas 1: GTM & GA4 Setup (Vecka 1)**

#### **Steg 1: Skapa GA4 Property för projektet**

1. Gå till Google Analytics: https://analytics.google.com
2. Skapa ny property: "[Projektnamn] - Web"
3. Konfigurera data streams:
   - Web stream: `projektets-domän.com`
   - Eventuellt: Android app stream (för framtida app)
   - Eventuellt: iOS app stream (för framtida app)
4. Spara Measurement ID (G-XXXXXXXXXX)

#### **Steg 2: Konfigurera GTM Web Container**

**Rekommenderat: Använd samma GTM container med routing**
- Använd samma GTM Web Container (GTM-PD5N4GT3)
- Lägg till hostname-routing i GTM
- Skicka events till rätt GA4 property baserat på hostname

**Se:** [GTM Shared Container](./GTM_SHARED_CONTAINER.md) för detaljerad guide

#### **Steg 3: Uppdatera projekt-kod**

**Se projekt-specifik dokumentation för implementation:**
- [flocken-website/docs/tracking/GTM_SETUP_INSTRUCTIONS.md](https://github.com/tbinho/flocken-website/tree/main/docs/tracking)
- [nastahem/docs/tracking/](https://github.com/tbinho/nastahem/tree/main/docs/tracking)

### **Fas 2: Server-side GTM (Vecka 2)**

**Rekommenderat: Använd samma server container med routing**
- Uppdatera GTM Server Container (GTM-THB49L3K)
- Lägg till hostname-routing
- Skicka till rätt GA4 property baserat på hostname

**Se:** [GTM Shared Container](./GTM_SHARED_CONTAINER.md) för detaljerad guide

### **Fas 3: BigQuery Integration (Vecka 3)**

**Se:** [BigQuery Shared Project](./BIGQUERY_SHARED_PROJECT.md) för detaljerad guide

**Projekt-specifik implementation:**
- [flocken-website/docs/bigquery/BIGQUERY_SETUP_INSTRUCTIONS.md](https://github.com/tbinho/flocken-website/tree/main/docs/bigquery)
- [nastahem/docs/bigquery/](https://github.com/tbinho/nastahem/tree/main/docs/bigquery)

---

## 📋 Implementation Checklist

### **Vecka 1: GTM & GA4 Setup**

- [ ] Skapa GA4 Property för projektet
- [ ] Spara Measurement ID (G-XXXXXXXXXX)
- [ ] Konfigurera GTM Web Container (se [GTM Shared Container](./GTM_SHARED_CONTAINER.md))
- [ ] Uppdatera projekt-kod (se projekt-specifik dokumentation)
- [ ] Konfigurera GA4 Configuration tag i GTM
- [ ] Konfigurera GA4 Event tags i GTM
- [ ] Testa event tracking i GA4 Realtime
- [ ] Verifiera att cookie consent fungerar

### **Vecka 2: Server-side GTM**

- [ ] Konfigurera GTM Server Container (se [GTM Shared Container](./GTM_SHARED_CONTAINER.md))
- [ ] Konfigurera GA4 Server tags
- [ ] Testa server-side tracking
- [ ] Verifiera data quality

### **Vecka 3: BigQuery Integration**

- [ ] Skapa BigQuery datasets (se [BigQuery Shared Project](./BIGQUERY_SHARED_PROJECT.md))
- [ ] Konfigurera GA4 BigQuery export
- [ ] Skapa SQL transformations (se projekt-specifik dokumentation)
- [ ] Testa data pipeline
- [ ] Skapa business intelligence queries

---

## 🔍 Vanliga Problem och Lösningar

### **Problem 1: gtag.js direkt istället för GTM**

**Problem:**
- Kan orsaka konflikter med GTM
- Svårt att underhålla
- Ingen centraliserad tag management

**Lösning:**
- Ersätt med GTM Web Container
- Hantera Google Ads via GTM istället

### **Problem 2: Ingen GA4**

**Lösning:**
- Skapa GA4 Property för projektet
- Konfigurera GTM → GA4 tracking

### **Problem 3: Ingen server-side tracking**

**Lösning:**
- Sätt upp GTM Server Container
- Konfigurera server-side routing

---

## ✅ Slutsats

**Denna setup är rekommenderad för alla Spitakolus-projekt:**

1. **✅ Professionell arkitektur** - Enterprise-grade tracking
2. **✅ Server-side tracking** - Bättre data quality och privacy
3. **✅ BigQuery integration** - Data warehouse för långsiktig analys
4. **✅ Cookie consent** - GDPR-compliant
5. **✅ Skalbar** - Redo för framtida app integration

**Rekommendation:** Implementera samma setup för alla projekt med:
- Separata GA4 Properties
- Separata BigQuery datasets
- GTM routing via shared container
- Samma server-side setup

---

## 📚 Relaterad dokumentation

- [GTM Shared Container](./GTM_SHARED_CONTAINER.md) - GTM container setup
- [BigQuery Shared Project](./BIGQUERY_SHARED_PROJECT.md) - BigQuery projekt setup
- [GA4 Property Structure](./GA4_PROPERTY_STRUCTURE.md) - GA4 best practices

**Projekt-specifik dokumentation:**
- [flocken-website/docs/tracking/](https://github.com/tbinho/flocken-website/tree/main/docs/tracking)
- [nastahem/docs/tracking/](https://github.com/tbinho/nastahem/tree/main/docs/tracking)

---

**Nästa steg:** Se [GTM Shared Container](./GTM_SHARED_CONTAINER.md) för att lägga till nytt projekt

