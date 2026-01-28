# Meta Ads Naming Conventions

**Detta dokument definierar naming conventions för Meta Ads som fungerar över flera konton och projekt.**

**Version:** 1.0  
**Status:** LÅST  
**Syfte:** Skapa ett skalbart, AI-vänligt och analysbart Meta Ads-system

---

## 0. Grundprinciper

- Endast tillåtna tecken: a–z, 0–9, _  
- Inga mellanslag  
- Inga specialtecken (+ | - : / @ å ä ö)  
- Alla objekt som hör ihop delar samma `cid`  
- `cid` är teknisk primärnyckel och ändras aldrig  
- Struktur är viktigare än "snygga namn"

---

## 1. CID – Campaign ID (Primärnyckel)

### Format  
```
cid001
cid002
cid003
```

### Regler  
- 3 siffror  
- Skapas när kampanjen skapas  
- Återanvänds aldrig  
- Finns på campaign, ad set och ad  
- Får aldrig ändras

### Syfte  
- Göra annonser identifierbara i platta listor, CSV-exporter och API-utdrag  
- Möjliggöra säker gruppering i analys, BI och automation

---

## 2. Campaign (C) – Strategi + Hypotes

### Definition  
En campaign representerar:  
- EN hypotes  
- EN målgrupp  
- ETT funnel-steg  
- ETT Meta-mål

### Format  
```
c_<app><geo><stage><aud><obj>_h<nn>_cid<nnn>
```

### Kontrollerad vokabulär (exempel - projekt-specifik)
- app: Projekt-specifik kod (t.ex. `flo`, `nas`)
- geo: Geografisk kod (t.ex. `swe`, `nor`)
- stage: Funnel-steg (t.ex. `init`, `rmk`)
- aud: Målgrupp (projekt-specifik, t.ex. `dogowner`, `sitter`, `biz`, `all`)
- obj: Mål (t.ex. `inst`, `eng`)
- hypotes: `h01`, `h02`, `h03` …

### Exempel (projekt-specifika)
```
c_flo_swe_init_dogowner_inst_h01_cid001
c_flo_swe_init_sitter_inst_h01_cid002
c_nas_swe_rmk_all_inst_h01_cid010
```

### Regel  
- Ny hypotes = ny campaign = nytt cid

---

## 3. Ad Set (AS) – Distributionscell

### Definition  
Ad set beskriver hur Meta distribuerar annonser.  
Innehåller INGEN kreativ information.

### Format  
```
as_<cell>_<geo>opt<obj>_cid<nnn>
```

### Kontrollerad vokabulär – cell  
- `broad` - Broad targeting
- `stack` - Stacked interests
- `lal01` - Lookalike 1%
- `rmk07` - Remarketing 7 dagar
- `rmk30` - Remarketing 30 dagar

### Exempel  
```
as_broad_swe_opt_inst_cid001
as_stack_swe_opt_inst_cid001
as_rmk30_swe_opt_inst_cid010
```

### Förbjudet i ad set  
- Hooks / funktioner  
- Kreativa idéer  
- Format eller dimensioner  
- Copy eller CTA

---

## 4. Ad (AD) – Idé + Variant + Hook

### Definition  
Ad-namnet ska vara begripligt även utan kampanjkontext (t.ex. i CSV).

### Format  
```
ad_h<nn><g>_cb<nnn>_v<nn>hk<token>src<token>_cid<nnn>
```

### Fält  
- h<nn><g>: hypotes + gren (ex h01a, h01b)  
- cb<nnn>: creative base  
- v<nn>: micro-variant (kosmetisk)  
- hk_<token>: hook/funktion (projekt-specifik)
- src_<token>: skapare (`ai`, `hum`)
- cid<nnn>: campaign id

### Kontrollerad vokabulär  
- hook: Projekt-specifik (t.ex. `all`, `para`, `passa`, `rasta`, `besoka`)
- source: `ai`, `hum`

### Exempel  
```
ad_h01a_cb003_v01_hk_besoka_src_ai_cid001
ad_h01a_cb003_v02_hk_besoka_src_ai_cid001
ad_h01b_cb007_v01_hk_all_src_hum_cid001
```

### Regler  
- Bokstav (a/b/c) = strategisk gren av hypotes  
- v01/v02 = micro-variation  
- Format/dimension får ALDRIG finnas i ad-namn

---

## 5. Analysprincip

- `cid` är primärnyckel i analys  
- Ads kan analyseras utan kampanjkontext  
- Campaign-namn kan ändras utan att bryta analys

---

## 6. AI / Cursor – Tillåtna handlingar

### FÅR  
- Skapa nya vXX under befintlig CB  
- Skapa nya CB under samma hypotes  
- Skapa ads med korrekt cid  
- Pausa alla objekt med ett specifikt cid

### FÅR INTE  
- Ändra cid  
- Flytta ads mellan cid  
- Skapa nya hypoteser utan beslut  
- Avvika från naming-spec

---

## 🔗 Projekt-specifik dokumentation

För projekt-specifik Meta Ads-struktur och vokabulär, se:
- [flocken-website/meta_ads_structure_flocken.md](https://github.com/tbinho/flocken-website/blob/main/meta_ads_structure_flocken.md) - Flocken-specifik struktur och vokabulär
- [flocken-website/docs/meta/](https://github.com/tbinho/flocken-website/tree/main/docs/meta) - Flocken-specifik Meta Ads-dokumentation

---

## 📖 Relaterad dokumentation

- [Creative Workflow](./CREATIVE_WORKFLOW.md) - Creative Bases och workflow
- [Account Structure](./ACCOUNT_STRUCTURE.md) - Kontostruktur

---

**Senast uppdaterad:** 2026-01-28
