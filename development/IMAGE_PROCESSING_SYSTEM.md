# Bildhanteringssystem - Gemensam Standard

**Detta dokument beskriver det gemensamma bildhanteringssystemet som används i alla Spitakolus-produkter.**

---

## 🎯 Översikt

Alla produkter använder ett Sharp-baserat bildhanteringssystem som:
- Konverterar bilder till optimerade format (AVIF, WebP, JPG)
- Genererar flera storlekar automatiskt
- Separerar original från genererade filer
- Håller metadata om processerade bilder

---

## 📁 Standard Mappstruktur

```
public/assets/[produkt]/
├── _originals/              # 📥 Originalbilder (högupplöst)
│   └── [produkt]_[typ]_[beskrivning].[ext]
│
├── generated/               # 📤 Auto-genererade optimerade bilder
│   └── [produkt]_[typ]_[beskrivning]_[storlek].[format]
│
├── screenshots/             # App/webb screenshots (manuella)
├── videos/                  # Videos
├── logo/                    # Logotyper
├── heroes/                  # Hero-bilder
└── icons/                   # Ikoner
```

**OBS:** Historiska projekt kan ha annan struktur (t.ex. `public/media/`). Nya produkter ska följa denna standard.

---

## 🏷️ Namngivningskonvention

### Format
```
[produkt]_[typ]_[beskrivning]_[dimension].[ext]
```

### Komponenter
| Del | Beskrivning | Exempel |
|-----|-------------|---------|
| `[produkt]` | Produktnamn | `flocken`, `nastahem` |
| `[typ]` | Bildtyp | `hero`, `screenshot`, `icon`, `image` |
| `[beskrivning]` | Vad bilden visar | `para-karta-alla-hundar` |
| `[dimension]` | Bildförhållande (valfritt) | `16x9`, `1x1`, `9x16` |

### Exempel
```
flocken_screenshot_para-karta-alla-hundar.png
flocken_hero_start_16x9.jpg
nastahem_screenshot_app-mobile-karta_9x16.png
nastahem_hero_guides-vardering_3x2.webp
```

---

## 🛠️ Image Processor

### Installation
```bash
npm install sharp
```

### Script-fil
Varje produkt har en `image-processor.js` i `scripts/`:
- flocken-website: `scripts/image-processor-flocken.js`
- nastahem: `scripts/image-processor.js`

### Kommandon
```bash
# Processa alla bilder i _originals/
node scripts/image-processor-[produkt].js process-all

# Processa en specifik bild
node scripts/image-processor-[produkt].js process path/to/image.jpg

# Visa status på bildbiblioteket
node scripts/image-processor-[produkt].js status

# Rensa genererade bilder
node scripts/image-processor-[produkt].js clean
```

---

## 📐 Genererade Storlekar

| Storlek | Bredd | Användning |
|---------|-------|------------|
| `thumbnail` | 150px | Miniatyrer, listor |
| `small` | 400px | Mobilvisning |
| `medium` | 800px | Tablet, cards |
| `large` | 1200px | Desktop |
| `xlarge` | 1920px | Hero, retina |

### Genererade Format
Varje storlek genereras i 3 format:
1. **AVIF** - Bäst komprimering, modern browser support
2. **WebP** - God komprimering, bred support
3. **JPG** - Fallback för äldre browsers

---

## 🔗 Använda bilder i kod

### Med Next.js Image (rekommenderat)
```tsx
import Image from 'next/image';

<Image
  src="/assets/flocken/generated/flocken_hero_start_large.webp"
  alt="Flocken"
  width={1200}
  height={800}
  priority // För hero-bilder
/>
```

### Med picture för format-fallback
```tsx
<picture>
  <source 
    srcSet="/assets/flocken/generated/flocken_hero_large.avif" 
    type="image/avif" 
  />
  <source 
    srcSet="/assets/flocken/generated/flocken_hero_large.webp" 
    type="image/webp" 
  />
  <img 
    src="/assets/flocken/generated/flocken_hero_large.jpg" 
    alt="Hero"
  />
</picture>
```

### Sökvägar
```
/assets/[produkt]/generated/[filnamn]_[storlek].[format]
```

---

## 📥 Workflow: Lägga till nya bilder

### 1. Namnge korrekt
```
[produkt]_[typ]_[beskrivning].[ext]
```

### 2. Lägg i _originals/
```bash
cp min-bild.jpg public/assets/flocken/_originals/flocken_hero_ny-sida.jpg
```

### 3. Kör image processor
```bash
node scripts/image-processor-flocken.js process-all
```

### 4. Använd i kod
```tsx
<Image src="/assets/flocken/generated/flocken_hero_ny-sida_large.webp" />
```

---

## ⚠️ Regler

1. **ALDRIG** lägg bilder direkt i `generated/` - de skrivs över
2. **ALLTID** använd produktprefix i filnamn
3. **ALLTID** kör `process-all` efter nya bilder
4. **UNDVIK** mellanslag i filnamn (använd bindestreck)
5. **BEHÅLL** original i `_originals/` för framtida omprocessering

---

## 🚀 Framtida förbättringar (TODO)

- [ ] Automatisk processing vid `npm run build`
- [ ] Watch mode för utveckling
- [ ] Responsive image srcset generator
- [ ] Blur placeholder generation
- [ ] CLI för att skapa ny produktstruktur

---

## 📚 Projekt-specifik dokumentation

- [flocken-website/IMAGE_MANAGEMENT.md](https://github.com/tbinho/flocken-website) - Flocken-specifika inställningar
- [nastahem/IMAGE_MANAGEMENT.md](https://github.com/tbinho/nastahem) - Nästa Hem-specifika inställningar

---

**Senast uppdaterad:** 2026-01-28
