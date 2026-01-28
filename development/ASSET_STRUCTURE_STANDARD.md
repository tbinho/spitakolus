# Asset-struktur Standard

**Detta dokument definierar den enhetliga asset-strukturen som ska användas i alla produkt-repos.**

---

## 🎯 Syfte

- Konsistent struktur över alla produkter
- Enkelt att lägga till nya bilder och content
- Lätt att sortera och hitta rätt
- Inga trasiga länkar vid flytt/duplicering

---

## 📁 Standard Asset-struktur

Varje produkt-repo ska ha följande struktur:

```
public/
└── assets/
    └── [produktnamn]/           # Produktens namn (t.ex. flocken, nastahem)
        ├── _originals/          # Originalbilder (högupplöst, ej processade)
        │   └── [bild].png/.jpg
        │
        ├── generated/           # Processade/optimerade bilder för webb
        │   └── [bild].[avif|webp|jpg|png]
        │
        ├── logo/                # Logotyper
        │   ├── logo_icon_[produkt]_large_1x1.png
        │   └── logo_icon_[produkt]_small_1x1.png
        │
        ├── screenshots/         # App/webb screenshots
        │   └── [produkt]_[funktion]_[beskrivning].png
        │
        ├── videos/              # Videos
        │   └── [produkt]_[funktion].mp4
        │
        ├── heroes/              # Hero-bilder för sidor
        │   └── [produkt]_hero_[sida].png
        │
        ├── icons/               # Ikoner
        │   └── [produkt]_icon_[namn].svg
        │
        └── email/               # Email-specifika bilder
            └── [produkt]_email_[typ].png
```

---

## 📝 Naming Convention

### Prefix med produktnamn
**ALLTID** börja filnamn med produktnamnet:
- ✅ `flocken_para_karta.png`
- ✅ `nastahem_hero_start.png`
- ❌ `para_karta.png`
- ❌ `hero_start.png`

### Format
```
[produkt]_[kategori]_[beskrivning]_[dimension].[ext]
```

**Exempel:**
- `flocken_screenshot_para-karta-alla-hundar.png`
- `flocken_hero_start_16x9.jpg`
- `nastahem_screenshot_app-mobile-karta_9x16.png`
- `nastahem_hero_guides-vardering_3x2.webp`

### Dimension (valfritt men rekommenderat)
- `_1x1` - Kvadrat
- `_16x9` - Widescreen
- `_9x16` - Mobil/vertikal
- `_3x2` - Standard foto
- `_4x5` - Instagram

### Använd snake_case
- ✅ `flocken_para_karta-alla-hundar.png`
- ❌ `flocken-para-karta-alla-hundar.png`
- ❌ `FlockenParaKarta.png`

---

## 🔗 Hur man refererar till assets i kod

### Alltid absolut sökväg från public/
```tsx
// ✅ RÄTT - Alltid börja med /assets/
<img src="/assets/flocken/screenshots/flocken_para_karta.png" />
<img src="/assets/nastahem/heroes/nastahem_hero_start.jpg" />

// ❌ FEL - Relativa sökvägar
<img src="./assets/flocken/para_karta.png" />
<img src="../public/assets/flocken/para_karta.png" />
```

### Video
```tsx
<video src="/assets/flocken/videos/flocken_para.mp4" />
```

### I CSS/Tailwind
```css
background-image: url('/assets/flocken/heroes/flocken_hero_start.jpg');
```

---

## 📥 Lägga till nya bilder - Workflow

### 1. Lägg original i `_originals/`
```bash
# Kopiera originalbild
cp min_nya_bild.png public/assets/flocken/_originals/flocken_hero_ny-sida.png
```

### 2. Processa för webb (om nödvändigt)
```bash
# Kör image processor (om tillgänglig)
node scripts/image-processor-flocken.js

# Eller manuellt optimera och lägg i generated/
```

### 3. Flytta till rätt undermapp
```bash
# Screenshots
mv public/assets/flocken/_originals/flocken_screenshot_*.png public/assets/flocken/screenshots/

# Heroes
mv public/assets/flocken/_originals/flocken_hero_*.png public/assets/flocken/heroes/
```

### 4. Använd i kod
```tsx
<img src="/assets/flocken/screenshots/flocken_screenshot_ny-funktion.png" />
```

---

## ⚠️ Viktigt att undvika

### ❌ Blanda produkter i samma mapp
```
public/assets/
├── flocken_bild.png     ❌ FEL
├── nastahem_bild.png    ❌ FEL
└── flocken/
    └── bild.png         ✅ RÄTT
```

### ❌ Generiska namn utan produktprefix
```
logo.png               ❌ FEL
hero.png               ❌ FEL
flocken_logo.png       ✅ RÄTT
nastahem_hero.png      ✅ RÄTT
```

### ❌ Mellanslag i filnamn
```
flocken para karta.png     ❌ FEL
flocken_para_karta.png     ✅ RÄTT
```

---

## 🔄 Migration från gammal struktur

### Om du har `public/media/` istället för `public/assets/[produkt]/`:

1. **Skapa ny struktur:**
   ```bash
   mkdir -p public/assets/[produkt]/{_originals,generated,screenshots,videos,heroes,logo}
   ```

2. **Flytta filer:**
   ```bash
   mv public/media/_originals/* public/assets/[produkt]/_originals/
   mv public/media/_generated/* public/assets/[produkt]/generated/
   ```

3. **Uppdatera alla referenser i kod:**
   - Sök efter `/media/` och ersätt med `/assets/[produkt]/`

4. **Testa att alla bilder laddas**

---

## 📋 Checklista för nya produkter

- [ ] Skapa `public/assets/[produkt]/` struktur
- [ ] Skapa undermappar: `_originals/`, `generated/`, `logo/`, `screenshots/`, `videos/`
- [ ] Namnge alla filer med produktprefix
- [ ] Använd snake_case
- [ ] Referera med absoluta sökvägar `/assets/[produkt]/...`
- [ ] Dokumentera specifika conventions i produktens `IMAGE_MANAGEMENT.md`

---

## 📚 Relaterad dokumentation

- [flocken-website/IMAGE_MANAGEMENT.md](https://github.com/tbinho/flocken-website) - Flocken-specifik bildhantering
- [PRODUCT_SEPARATION_GUIDE.md](./PRODUCT_SEPARATION_GUIDE.md) - Multi-repo struktur

---

**Senast uppdaterad:** 2026-01-28
