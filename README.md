# Spitakolus - Företagsgemensam Dokumentation

**⚠️ VIKTIGT:** Detta är **FÖRETAGSGEMENSAM** dokumentation för Spitakolus AB.  
Detta repo innehåller delad dokumentation som används av flera projekt.

**För projekt-specifik dokumentation, se:**
- [flocken-website](https://github.com/tbinho/flocken-website) - Flocken projekt
- [nastahem](https://github.com/tbinho/nastahem) - Nästa Hem projekt

---

## 🎯 Vad finns här?

Detta repo innehåller **delad dokumentation** som används av flera projekt:

- **Delad tracking-infrastruktur** (GTM Shared Container, BigQuery projekt)
- **Delade Meta Ads standarder** (naming conventions, workflows)
- **Företagsövergripande processer** (Git workflows, deployment-standarder)
- **Regler för dokumentation** (hur man dokumenterar, uppdaterar, indexerar)
- **Mallar för nya repos** (templates för att säkerställa konsistent struktur)

---

## 📁 Struktur

```
spitakolus/
├── README.md                          # Denna fil
├── DOCUMENTATION_RULES.md             # Regler för dokumentation
│
├── tracking/                          # Delad tracking-infrastruktur
│   ├── README.md                     # Index för tracking-dokumentation
│   ├── GTM_SHARED_CONTAINER.md       # GTM container som delas
│   ├── BIGQUERY_SHARED_PROJECT.md    # BigQuery projekt-struktur
│   └── SHARED_EVENTS_CONVENTIONS.md  # Event naming som delas
│
├── meta-ads/                         # Delade Meta Ads standarder
│   ├── README.md                     # Index för Meta Ads-dokumentation
│   ├── NAMING_CONVENTIONS.md         # Naming conventions (fungerar över flera konton)
│   ├── CREATIVE_WORKFLOW.md          # Creative workflow (delas mellan projekt)
│   └── ACCOUNT_STRUCTURE.md          # Hur konton ska struktureras
│
├── development/                       # Företagsövergripande utveckling
│   ├── README.md                     # Index för development-dokumentation
│   ├── GIT_WORKFLOW.md               # Företagsövergripande Git-standarder
│   ├── DEPLOYMENT_STANDARDS.md       # Deployment-standarder
│   └── TEMPLATES/                    # Mallar för nya repos
│       ├── README_TEMPLATE.md
│       └── DOCUMENTATION_MAP_TEMPLATE.md
│
└── company/                          # Företagsinformation
    ├── README.md
    ├── COMPANY_INFO.md               # Spitakolus AB info
    └── CONTACT.md                    # Kontaktinformation
```

---

## 🚀 Start här

### För att förstå delad infrastruktur:
1. **[tracking/README.md](./tracking/README.md)** - Delad tracking-infrastruktur
2. **[meta-ads/README.md](./meta-ads/README.md)** - Delade Meta Ads standarder
3. **[development/README.md](./development/README.md)** - Företagsövergripande processer

### För att skapa nya repos:
1. **[DOCUMENTATION_RULES.md](./DOCUMENTATION_RULES.md)** - Regler för dokumentation
2. **[development/TEMPLATES/](./development/TEMPLATES/)** - Mallar för nya repos

---

## 📋 Viktiga principer

### Delad dokumentation vs Projekt-specifik

**Delad dokumentation (här i spitakolus):**
- ✅ Används av flera projekt
- ✅ Företagsövergripande standarder
- ✅ Delad infrastruktur (GTM, BigQuery)
- ✅ Processer som delas mellan projekt

**Projekt-specifik dokumentation (i projekt-repos):**
- ✅ Specifik för ett projekt
- ✅ Projekt-specifik deployment
- ✅ Projekt-specifika workflows
- ✅ Projekt-specifika kampanjer

### När ska dokumentation vara här?

**Placera dokumentation här om:**
- Det gäller flera projekt (t.ex. GTM Shared Container)
- Det är företagsövergripande standarder
- Det är processer som används i flera projekt
- Det är infrastruktur som delas (t.ex. BigQuery projekt)

**Placera dokumentation i projekt-repo om:**
- Det är specifikt för ett projekt
- Det är deployment-instruktioner för ett specifikt repo
- Det är projekt-specifika workflows
- Det är projekt-specifika kampanjer eller kreativt arbete

---

## 🔗 Länkar till projekt-repos

- **[flocken-website](https://github.com/tbinho/flocken-website)** - Flocken projekt
- **[nastahem](https://github.com/tbinho/nastahem)** - Nästa Hem projekt

---

## 📖 Regler för dokumentation

Se [DOCUMENTATION_RULES.md](./DOCUMENTATION_RULES.md) för:
- Hur man dokumenterar
- När man uppdaterar
- Hur man indexerar
- Var man lägger ny dokumentation
- Mallar för nya repos

---

**Senast uppdaterad:** 2026-01-28
