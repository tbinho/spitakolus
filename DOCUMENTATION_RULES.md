# Regler för Dokumentation - Spitakolus AB

**Datum:** 2026-01-28  
**Syfte:** Regler och best practices för hur dokumentation ska skapas, uppdateras och indexeras

---

## 🎯 Översikt

Detta dokument definierar regler för dokumentation i alla Spitakolus-repos:
- **spitakolus** - Företagsgemensam dokumentation (detta repo)
- **flocken-website** - Projekt-specifik dokumentation
- **nastahem** - Projekt-specifik dokumentation
- **Framtida repos** - Projekt-specifik dokumentation

---

## 📋 Grundläggande regler

### 1. Varje repo måste ha

**Obligatoriskt i varje repo-root:**
- ✅ **README.md** med tydlig varning: "Detta är [PROJEKTNAMN] repo"
- ✅ **DOCUMENTATION_MAP.md** med komplett översikt över ALL dokumentation
- ✅ **Länkar till spitakolus** för delad dokumentation
- ✅ **Länkar till andra projekt-repos** för jämförelse

**Exempel varning i README.md:**
```markdown
**⚠️ VIKTIGT:** Detta är **FLOCKEN-WEBSITE** repo.  
För Nästa Hem-projektet, se [nastahem](https://github.com/tbinho/nastahem).
```

### 2. Dokumentationsstruktur

**Företagsgemensamt (spitakolus):**
- Delad infrastruktur (GTM, BigQuery)
- Företagsövergripande standarder
- Processer som delas mellan projekt
- Mallar för nya repos

**Projekt-specifik (flocken-website, nastahem, etc.):**
- Projekt-specifik setup och konfiguration
- Projekt-specifik deployment
- Projekt-specifika workflows
- Projekt-specifika kampanjer

### 3. Naming conventions

**Filer:**
- ✅ Beskrivande namn (inte "doc1.md")
- ✅ Versaler för viktiga filer (README.md, DOCUMENTATION_MAP.md)
- ✅ Konsekvent struktur över repos

**Mappar:**
- ✅ Beskrivande namn (`tracking/`, `meta-ads/`, `development/`)
- ✅ Konsistent struktur över repos

---

## 📝 Hur man dokumenterar

### När ska dokumentation skapas?

**Skapa dokumentation när:**
- ✅ Ny funktionalitet implementeras
- ✅ Ny process etableras
- ✅ Setup-instruktioner behövs
- ✅ Troubleshooting-guide behövs
- ✅ Best practices identifieras

**Uppdatera dokumentation när:**
- ✅ Processer ändras
- ✅ Setup-instruktioner ändras
- ✅ Nya steg läggs till
- ✅ Fel hittas i dokumentationen

### Var ska dokumentation ligga?

**I spitakolus (delad dokumentation):**
- Om det gäller flera projekt
- Om det är företagsövergripande standarder
- Om det är delad infrastruktur

**I projekt-repo (projekt-specifik):**
- Om det är specifikt för ett projekt
- Om det är projekt-specifik deployment
- Om det är projekt-specifika workflows

### Hur strukturerar man dokumentation?

**För nya dokument:**
1. Bestäm om det är delat eller projekt-specifikt
2. Välj rätt repo och mapp
3. Följ befintlig struktur och naming conventions
4. Lägg till länkar i relevanta README.md
5. Uppdatera DOCUMENTATION_MAP.md om nödvändigt

---

## 🔄 Hur man uppdaterar dokumentation

### Uppdateringsprocess

1. **Identifiera vad som behöver uppdateras**
   - Processer som ändrats?
   - Setup-instruktioner som är utdaterade?
   - Nya steg som behövs?

2. **Uppdatera dokumentet**
   - Behåll struktur och format
   - **ALLTID uppdatera "Senast uppdaterad" datum**
   - Lägg till changelog om större ändringar

3. **Uppdatera länkar**
   - Uppdatera DOCUMENTATION_MAP.md om nödvändigt
   - Uppdatera README.md om strukturen ändras
   - Kontrollera att alla länkar fungerar

4. **Verifiera**
   - Läs igenom dokumentationen
   - Kontrollera att instruktioner är korrekta
   - Testa länkar

---

## 🗑️ Rensning och underhåll

### ❌ TA BORT utdaterad dokumentation

**Släng filer som:**
- ❌ Är äldre än 3 månader utan uppdatering
- ❌ Refererar till projekt/kod som inte längre finns
- ❌ Har flera versioner (behåll endast senaste)
- ❌ Är "cleanup plans" eller "migration plans" som slutförts
- ❌ Är temporära arbetsdokument

**Arkivera INTE allt - radera det som inte behövs!**

### ⚠️ Undvik duplicering

**ALDRIG:**
- ❌ Samma information på flera ställen
- ❌ Projekt-specifik dokumentation i fel repo
- ❌ Flocken-dokumentation i nastahem (eller vice versa)

**ALLTID:**
- ✅ En källa för varje typ av information
- ✅ Länka istället för att duplicera
- ✅ Flytta/ta bort vid omorganisering

### Underhållsrutin (månatlig)

1. Granska alla filer äldre än 2 månader
2. Ta bort utdaterade filer
3. Uppdatera brutna länkar
4. Verifiera att struktur matchar DOCUMENTATION_MAP.md

---

## 📚 Hur man indexerar dokumentation

### README.md i varje mapp

Varje mapp med dokumentation ska ha en README.md som:
- ✅ Förklarar vad som finns i mappen
- ✅ Listar alla dokument med länkar
- ✅ Förklarar läsordning
- ✅ Länkar till relaterad dokumentation

### DOCUMENTATION_MAP.md i varje repo

Varje projekt-repo ska ha en DOCUMENTATION_MAP.md som:
- ✅ Ger komplett översikt över ALL dokumentation
- ✅ Separerar projekt-specifik vs delad dokumentation
- ✅ Länkar till allt
- ✅ Innehåller varningar för AI om vilket repo det är

### Indexering i spitakolus

Spitakolus README.md ska:
- ✅ Förklara vad som finns i varje kategori
- ✅ Länka till alla viktiga dokument
- ✅ Förklara när dokumentation ska vara här vs i projekt-repos

---

## 🆕 Mallar för nya repos

### När ett nytt repo skapas

**Använd mallar från:**
- `spitakolus/development/TEMPLATES/README_TEMPLATE.md`
- `spitakolus/development/TEMPLATES/DOCUMENTATION_MAP_TEMPLATE.md`

**Checklista:**
- [ ] README.md med tydlig varning om vilket repo det är
- [ ] DOCUMENTATION_MAP.md med komplett översikt
- [ ] Länkar till spitakolus för delad dokumentation
- [ ] Länkar till andra projekt-repos
- [ ] Tydlig deployment-information
- [ ] Varningar för AI om vilket repo det är

---

## ⚠️ Viktiga påminnelser

### För AI-assistenter

**Varje repo måste tydligt förklara:**
- Vilket repo det är
- Vad som finns där
- Var delad dokumentation finns
- Var andra projekt-repos finns
- Vilken remote som ska användas för deployment

### För utvecklare

**När du dokumenterar:**
- Tänk på vem som läser (utvecklare, AI-assistenter)
- Var tydlig och specifik
- Uppdatera länkar när strukturen ändras
- Följ befintliga mönster

---

## 📋 Checklista för ny dokumentation

När du skapar ny dokumentation:

- [ ] Bestämt om det är delat eller projekt-specifikt
- [ ] Valit rätt repo och mapp
- [ ] Följt naming conventions
- [ ] Lagt till i relevant README.md
- [ ] Uppdaterat DOCUMENTATION_MAP.md om nödvändigt
- [ ] Lagt till datum och författare
- [ ] Verifierat att länkar fungerar
- [ ] Läs igenom för tydlighet

---

## 🔗 Relaterad dokumentation

- [README.md](./README.md) - Översikt över spitakolus repo
- [development/TEMPLATES/](./development/TEMPLATES/) - Mallar för nya repos
- [flocken-website/DOCUMENTATION_MAP.md](https://github.com/tbinho/flocken-website/blob/main/DOCUMENTATION_MAP.md) - Exempel på projekt-specifik dokumentationskarta

---

**Senast uppdaterad:** 2026-01-28
