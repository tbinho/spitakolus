# BigQuery Shared Project - Setup och Best Practices

**Detta dokument beskriver det delade BigQuery-projektet (`nastahem-tracking`) som används av flera projekt.**

---

## 🎯 Översikt

Spitakolus-projekt använder ett **delat BigQuery-projekt** för att lagra och analysera tracking-data från alla projekt.

### Projekt Information

- **Project ID:** `nastahem-tracking`
- **Location:** EU (europe-west1)
- **Strategi:** Delat projekt med separata datasets per projekt

---

## 📊 Projektstruktur

### Dataset Structure

```
nastahem-tracking/
├── nastahem_raw/              # Nästa Hem raw data
│   └── events_YYYYMMDD
├── nastahem_curated/          # Nästa Hem processed
│   └── events
├── nastahem_marts/            # Nästa Hem business metrics
│   └── daily_metrics
│
├── flocken_raw/               # Flocken raw data
│   └── events_YYYYMMDD
├── flocken_curated/           # Flocken processed
│   └── events
└── flocken_marts/             # Flocken business metrics
    └── daily_metrics
```

### Princip: Separata datasets per projekt

Varje projekt har sina egna datasets:
- `[projekt]_raw` - Raw GA4 export data
- `[projekt]_curated` - Processed events
- `[projekt]_marts` - Business intelligence metrics

---

## 🚀 Lägga till nytt projekt i BigQuery

### Steg 1: Skapa datasets för nytt projekt

**I BigQuery Console:**

1. Gå till: https://console.cloud.google.com/bigquery
2. Välj project: `nastahem-tracking`
3. Klicka på "Compose New Query"
4. Kör följande SQL:

```sql
-- Skapa datasets för nytt projekt
CREATE SCHEMA IF NOT EXISTS `nastahem-tracking.[projekt]_raw`
  OPTIONS(
    description='Raw GA4 export data for [Projektnamn]',
    location='EU'
  );

CREATE SCHEMA IF NOT EXISTS `nastahem-tracking.[projekt]_curated`
  OPTIONS(
    description='Cleaned and standardized [Projektnamn] events',
    location='EU'
  );

CREATE SCHEMA IF NOT EXISTS `nastahem-tracking.[projekt]_marts`
  OPTIONS(
    description='Business intelligence ready [Projektnamn] metrics',
    location='EU'
  );
```

### Steg 2: Konfigurera GA4 BigQuery Export

1. Gå till GA4 Property → Admin → BigQuery Linking
2. Välj GCP Project: `nastahem-tracking`
3. Välj Location: **EU (europe-west1)**
4. Aktivera Daily Export
5. Aktivera Streaming Export (rekommenderat)
6. Destination: `[projekt]_raw` dataset
7. Klicka på "Submit"

### Steg 3: Verifiera data export

**Vänta på första export:**
- Daily export körs vanligtvis kl 04:00 UTC
- Streaming export börjar omedelbart (men kan ta några minuter)

**Kontrollera i BigQuery:**
```sql
-- Test query för att verifiera data
SELECT 
  event_date,
  COUNT(*) as event_count,
  COUNT(DISTINCT user_pseudo_id) as unique_users
FROM `nastahem-tracking.[projekt]_raw.events_*`
WHERE _TABLE_SUFFIX >= FORMAT_DATE('%Y%m%d', DATE_SUB(CURRENT_DATE(), INTERVAL 7 DAY))
GROUP BY event_date
ORDER BY event_date DESC
LIMIT 10;
```

---

## 📋 Best Practices

### 1. Dataset naming convention

**Format:** `[projekt]_[typ]`

**Exempel:**
- `flocken_raw`
- `flocken_curated`
- `flocken_marts`
- `nastahem_raw`
- `nastahem_curated`
- `nastahem_marts`

### 2. Location: Alltid EU

**Alla datasets ska skapas med location EU:**
```sql
OPTIONS(location='EU')
```

**Varför:**
- GDPR-compliance
- Data lagras inom EU
- Bättre prestanda för EU-användare

### 3. Dataset structure

**Raw dataset:**
- Innehåller raw GA4 export data
- Tabeller: `events_YYYYMMDD` (daily export)
- Tabeller: `events_intraday_YYYYMMDD` (streaming export)

**Curated dataset:**
- Processed events med standardiserade fält
- Views och tables för cleaned data
- Cross-platform user stitching

**Marts dataset:**
- Business intelligence ready metrics
- Aggregerade data för dashboards
- Daily/weekly/monthly aggregations

---

## 🔧 Service Account Setup

### Skapa Service Account för nytt projekt

1. Gå till: https://console.cloud.google.com/iam-admin/serviceaccounts
2. Välj project: `nastahem-tracking`
3. Klicka på "Create Service Account"
4. **Service Account Details:**
   - Name: `[projekt]-bigquery-access`
   - Description: "Service account for [Projektnamn] BigQuery access"
5. **Grant Access:**
   - Role: `BigQuery Data Editor`
   - Role: `BigQuery Job User`
6. Klicka på "Done"
7. **Create Key:**
   - Klicka på service account → "Keys" → "Add Key" → "Create new key"
   - Key type: JSON
   - Spara JSON-filen säkert

### Använda Service Account Key

**I scripts:**
```javascript
const { BigQuery } = require('@google-cloud/bigquery');
const bigquery = new BigQuery({
  projectId: 'nastahem-tracking',
  keyFilename: 'path/to/service-account-key.json'
});
```

**Environment variable:**
```bash
export GOOGLE_APPLICATION_CREDENTIALS="path/to/service-account-key.json"
```

---

## 📊 Query Examples

### Cross-project queries

**Jämföra data mellan projekt:**
```sql
-- Jämför events mellan projekt
SELECT 
  CASE 
    WHEN _TABLE_SUFFIX LIKE 'nastahem%' THEN 'Nästa Hem'
    WHEN _TABLE_SUFFIX LIKE 'flocken%' THEN 'Flocken'
  END AS project,
  event_date,
  COUNT(*) AS events
FROM `nastahem-tracking.*.events_*`
WHERE _TABLE_SUFFIX >= FORMAT_DATE('%Y%m%d', DATE_SUB(CURRENT_DATE(), INTERVAL 30 DAY))
GROUP BY project, event_date
ORDER BY event_date DESC;
```

### Projekt-specifik queries

**Se projekt-specifik dokumentation:**
- [flocken-website/docs/bigquery/](https://github.com/tbinho/flocken-website/tree/main/docs/bigquery)
- [nastahem/docs/bigquery/](https://github.com/tbinho/nastahem/tree/main/docs/bigquery)

---

## 🔗 Projekt-specifik dokumentation

För projekt-specifik BigQuery-setup, se:
- [flocken-website/docs/bigquery/BIGQUERY_SETUP_INSTRUCTIONS.md](https://github.com/tbinho/flocken-website/tree/main/docs/bigquery)
- [nastahem/docs/bigquery/](https://github.com/tbinho/nastahem/tree/main/docs/bigquery)

---

## 📖 Relaterad dokumentation

- [GTM Shared Container](./GTM_SHARED_CONTAINER.md) - GTM container setup
- [GA4 Property Structure](./GA4_PROPERTY_STRUCTURE.md) - GA4 best practices

---

**Senast uppdaterad:** 2026-01-28
