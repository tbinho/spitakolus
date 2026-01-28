# GTM Shared Container - Setup och Best Practices

**Detta dokument beskriver den delade Google Tag Manager container som används av flera projekt.**

---

## 🎯 Översikt

Spitakolus-projekt använder en **delad GTM container** med hostname-based routing för att separera data mellan projekt.

### Container Information

- **Web Container ID:** `GTM-PD5N4GT3`
- **Server Container ID:** `GTM-THB49L3K`
- **Server Container URL:** `https://gtm.nastahem.com`
- **Strategi:** Shared container med hostname-based routing

---

## 📊 Arkitektur

### Container Structure

```
GTM-PD5N4GT3 (Shared Web Container)
├── Tags
│   ├── GA4 Configuration - Flocken
│   │   ├── Type: Google-tagg
│   │   ├── Tag ID: G-7B1SVKL89Q
│   │   ├── Trigger: Page View - Flocken
│   │   └── Condition: Page Hostname equals flocken.info
│   │
│   └── GA4 Configuration - Nästa Hem
│       ├── Type: Google-tagg
│       ├── Tag ID: G-7N67P0KT0B
│       ├── Trigger: Page View - Nästa Hem
│       └── Condition: Page Hostname equals nastahem.com
│
└── Triggers
    ├── Page View - Flocken
    │   ├── Type: Page View
    │   └── Condition: Page Hostname equals flocken.info
    │
    └── Page View - Nästa Hem
        ├── Type: Page View
        └── Condition: Page Hostname equals nastahem.com
```

---

## 🔧 Hostname Routing

### Hur routing fungerar

GTM använder **Page Hostname** condition för att skilja mellan projekt:

- **Nästa Hem tags:** Page Hostname equals `nastahem.com`
- **Flocken tags:** Page Hostname equals `flocken.info`

Detta säkerställer att:
- Nästa Hem events → Nästa Hem GA4 (G-7N67P0KT0B)
- Flocken events → Flocken GA4 (G-7B1SVKL89Q)

### Fördelar med shared container

- ✅ En GTM container för alla projekt (lättare underhåll)
- ✅ Tydlig separation av data
- ✅ Skalbart för fler projekt framåt
- ✅ Konsistent setup över projekt

---

## 🚀 Lägga till nytt projekt i shared container

### Steg 1: Skapa GA4 Property för nytt projekt

1. Gå till Google Analytics: https://analytics.google.com
2. Skapa ny property för projektet
3. Spara Measurement ID (G-XXXXXXXXXX)

### Steg 2: Skapa Google Tag i GTM Web Container

1. Gå till GTM: https://tagmanager.google.com
2. Välj container: **GTM-PD5N4GT3**
3. Klicka på "Tags" → "New"
4. **Tag Configuration:**
   - Tag Type: **Google-tagg** (Google Tag)
   - Tag ID: `G-XXXXXXXXXX` (projektets GA4 Measurement ID)
5. **Triggering:**
   - Trigger Type: **All Pages**
   - **Lägg till condition:**
     - Condition: **Page Hostname** equals `projektets-domän.com`
6. **Tag Name:** "Google Tag - [Projektnamn]"
7. Spara och publicera

### Steg 3: Konfigurera Server Container (om server-side tracking används)

1. Gå till GTM Server Container: **GTM-THB49L3K**
2. Skapa GA4 Configuration - Server tag för projektet
3. Measurement ID: `G-XXXXXXXXXX` (projektets GA4)
4. Trigger: Skapa ny trigger "All Events - [Projektnamn]"
   - Trigger Type: All Events
   - Condition: `Page Hostname equals projektets-domän.com`
5. Tag Name: "GA4 Server - [Projektnamn]"
6. Spara

---

## 🔐 Consent Mode v2

### Standard Consent Configuration

Alla projekt använder Consent Mode v2:

```javascript
window.dataLayer.push({
  'event': 'consent_default',
  'analytics_storage': 'denied',
  'ad_storage': 'denied',
  'ad_user_data': 'denied',
  'ad_personalization': 'denied',
  'functionality_storage': 'granted',
  'security_storage': 'granted'
});
```

### Consent Controls i GTM Tags

Varje Google Tag ska ha följande consent controls:
- `ad_storage` ✅
- `ad_personalization` ✅
- `ad_user_data` ✅
- `analytics_storage` ✅

### Server Consent URL

- **Server Consent URL:** `https://gtm.nastahem.com`

---

## 📚 Best Practices

### 1. Alltid använd hostname conditions

**✅ RÄTT:**
- Trigger condition: `Page Hostname equals flocken.info`
- Trigger condition: `Page Hostname equals nastahem.com`

**❌ FEL:**
- Inga conditions (alla tags triggas på alla sidor)
- URL-baserade conditions (mindre tillförlitligt)

### 2. Konsistent tag naming

**Format:** `[Tag Type] - [Projektnamn]`

**Exempel:**
- "Google Tag - Flocken"
- "GA4 Event - Flocken"
- "Google Ads Conversion - Nästa Hem"

### 3. Separera projekt-specifik konfiguration

- Varje projekt har egen GA4 Measurement ID
- Varje projekt har egen trigger med hostname condition
- Projekt-specifik konfiguration dokumenteras i projekt-repo

---

## 🔗 Projekt-specifik dokumentation

För projekt-specifik GTM-setup, se:
- [flocken-website/docs/tracking/GTM_SETUP_INSTRUCTIONS.md](https://github.com/tbinho/flocken-website/tree/main/docs/tracking)
- [nastahem/docs/tracking/](https://github.com/tbinho/nastahem/tree/main/docs/tracking)

---

## 📖 Relaterad dokumentation

- [GA4 Property Structure](./GA4_PROPERTY_STRUCTURE.md) - Best practices för GA4 properties
- [Google Analytics Evaluation](./GOOGLE_ANALYTICS_EVALUATION.md) - Utvärdering av tracking-setup

---

**Senast uppdaterad:** 2026-01-28
