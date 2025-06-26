# 🗺️ Chalmers Social Media Analytics - MapLibre Visualization

En avancerad interaktiv karta för visualisering av Chalmers social media-data med mörkt tema och professionella animationer.

![MapLibre Visualization](https://via.placeholder.com/800x500/0a0a0a/00f2ff?text=Chalmers+Social+Media+Analytics)

## 🚀 Snabbstart

### 1. **Öppna visualiseringen**
```bash
cd "/Users/theatornqvist/SoMe ClaudeCode"
open chalmers_maplibre_visualization.html
```

### 2. **Krav**
- ✅ Modern webbläsare (Chrome, Firefox, Safari, Edge)
- ✅ `chalmers_social_media_maplibre.geojson` i samma mapp
- ✅ Internetanslutning (för karttiles och bibliotek)

## 🎨 **Design Features**

### **Mörkt tema med neon-accenter**
- **Bakgrund**: Djupsvart (#0a0a0a) med glassmorphism-paneler
- **Neon-färger**: 
  - 🔵 Cyan (#00f2ff) - Positiv sentiment & UI-accenter
  - 🟢 Grön (#00ff88) - Positiv sentiment & framgång
  - 🔴 Rosa (#ff0055) - Negativ sentiment & varningar
  - 🟣 Lila (#8b5cf6) - Neutral sentiment & sekundära element

### **Glassmorphism-effekter**
- Halvtransparenta paneler med blur-effekt
- Subtila kantlinjer och skuggor
- Smooth hover-animationer med glöd-effekter

## 📊 **Visualiseringslägen**

### 1. **🔴 Punkter** (Standard)
- Färgkodade cirklar baserat på sentiment
- Glöd-effekt runt punkterna
- Skalning baserat på zoom-nivå
- **Grön** = Positiv sentiment
- **Röd** = Negativ sentiment  
- **Grå** = Neutral sentiment

### 2. **🔥 Värmekarta**
- Visar koncentration av inlägg
- Viktad efter räckvidd (reach)
- Dynamisk färggradient från blå till vit
- Bäst för att identifiera hotspots

### 3. **🧊 3D-extrudering**
- Höjd baserad på räckvidd
- 3D-visualisering av impact
- Pitch: 45° för optimal vy
- Imponerande för presentationer

### 4. **🗂️ Kluster**
- Grupperar närliggande punkter
- Färgkodade efter antal (blå → gul → röd)
- Klickbara för zoom-in
- Optimerat för performance

## ⏱️ **Tidslinje-animation**

### **Kontroller**
- ▶️ **Play/Pause**: Animerar data kronologiskt
- 🎚️ **Skrubb**: Dra för manuell navigering
- 📅 **Datum-display**: Visar aktuellt datum
- 📊 **Statistik**: Visar antal inlägg (aktuella/totala)

### **Keyboard Shortcuts**
- **Space**: Play/Pause animation
- **F**: Fullskärmsläge
- **E**: Exportera filtrerad data som CSV

### **Hastighet**
- Animationen går igenom all data på ~2 minuter
- Justerbar hastighet (ändra `timelinePosition += 0.001` i koden)

## 🔍 **Filter & Sök**

### **Sentiment-filter**
- ✅ **Positiv**: Visa positiva inlägg (grön)
- ✅ **Negativ**: Visa negativa inlägg (röd)  
- ✅ **Neutral**: Visa neutrala inlägg (grå)
- Klicka för att aktivera/avaktivera

### **Käll-filter**
- Dropdown med alla tillgängliga källor
- Twitter, Instagram, Facebook, etc.
- "Alla källor" för att visa allt

### **Nyckelords-sökning**
- Sök i titel, brödtext och nyckelord
- Real-time filtrering med 500ms debounce
- Case-insensitive sökning

### **Datumintervall**
- Välj start- och slutdatum
- Automatiskt ifyllt med data-intervallet
- Kombineras med andra filter

## 📈 **Statistik-dashboard**

### **Snabbstatistik**
- **Totalt inlägg**: Antal synliga datapunkter
- **Total räckvidd**: Summerad reach för alla inlägg
- **Positiv sentiment**: Procent positiva inlägg

### **Diagram**
- **🍩 Sentiment-fördelning**: Donut-diagram (positiv/negativ/neutral)
- **📊 Geografisk fördelning**: Top 5 platser
- **📈 Källfördelning**: Pie-chart över sociala medier

## 🖱️ **Interaktioner**

### **Hover-effekter**
- **Muspekare över punkt**: Tooltip med grundinfo
  - Titel, källa, datum, räckvidd
- **Smooth animationer**: 60fps hover-effekter
- **Glöd-effekter**: Neon-highlighting

### **Klick-interaktioner**
- **Klick på punkt**: Detaljerad popup med:
  - 📋 Fullständig titel och text
  - 📅 Datum och plats
  - 📊 Räckvidd och AVE-värde
  - 🔗 Länk till original
  - 📤 Dela-funktionalitet

- **Klick på kluster**: Zooma in för att expandera

### **Popup-funktioner**
- **Glassmorphism-design**: Halvtransparent med blur
- **Responsiv layout**: Anpassas efter innehåll
- **Sentiment-indikator**: Färgad cirkel
- **Statistik-rutor**: Reach och AVE i separata boxar
- **Action-knappar**: Visa original och dela

## 🎯 **Performance-optimering**

### **WebGL-rendering**
- 60fps smooth animationer
- Hardware-accelererad grafik
- Efficient rendering av många punkter

### **Clustering**
- Automatic clustering för förbättrad performance
- Dynamisk kluster-radie baserat på zoom
- Max zoom 14 för kluster

### **Lazy loading**
- Chart.js laddas endast när behövs
- Debounced filter-uppdateringar
- Efficient data-filtrering

### **Caching**
- Browser-cache för karttiles
- Minimala API-anrop
- Optimerad data-struktur

## 📱 **Responsiv design**

### **Desktop** (1200px+)
- Tre-kolumn layout
- Sidebar, karta, statistik
- Full funktionalitet synlig

### **Tablet** (768px - 1199px)
- Sidebar och statistik som overlays
- Toggle-knappar för paneler
- Karta i centrum

### **Mobile** (< 768px)
- Enkel-kolumn layout
- Komprimerade kontroller
- Touch-optimerade interaktioner
- Mindre typsnitt och knappar

## 🔧 **Anpassning**

### **Färger**
```css
:root {
    --neon-cyan: #00f2ff;     /* Cyan accent */
    --neon-green: #00ff88;    /* Positive */
    --neon-pink: #ff0055;     /* Negative */
    --neon-purple: #8b5cf6;   /* Neutral */
}
```

### **Animationshastighet**
```javascript
// I startAnimation() funktionen
timelinePosition += 0.001; // Öka för snabbare, minska för långsammare
```

### **Kluster-inställningar**
```javascript
map.addSource('chalmers-data', {
    cluster: true,
    clusterMaxZoom: 14,    // Max zoom för kluster
    clusterRadius: 50      // Kluster-radie i pixlar
});
```

### **Heatmap-intensitet**
```javascript
'heatmap-weight': [
    'interpolate',
    ['linear'],
    ['get', 'reach'],
    0, 0,
    1000, 1    // Justera max reach för viktning
]
```

## 🚨 **Felsökning**

### **Vanliga problem**

#### ❌ "Kunde inte ladda data"
- Kontrollera att `chalmers_social_media_maplibre.geojson` finns i samma mapp
- Öppna Developer Tools (F12) för att se felmeddelanden
- Verifiera att GeoJSON-filen är giltig

#### ❌ Karta laddas inte
- Kontrollera internetanslutning (behövs för Carto-tiles)
- Kolla att MapLibre GL JS laddas korrekt
- Öppna i en annan webbläsare

#### ❌ Diagram visas inte
- Chart.js kanske inte laddats - kontrollera nätverksfliken
- Kontrollera att data innehåller nödvändiga properties

#### ❌ Animationer laggar
- Stäng andra webbläsarflikar
- Kontrollera GPU-acceleration i webbläsaren
- Minska data-mängden med filter

### **Debug-läge**
Öppna Developer Console (F12) för att se:
- Data-laddningsstatus
- Filter-resultatsstatistik  
- Performance-mätningar
- Fel och varningar

## 🎪 **Demo-scenario**

### **För Chalmers-presentation:**

1. **🎬 Öppningsscen**
   - Starta i punktvy med alla filter aktiva
   - Zooma ut för att visa Sverige/internationell spridning
   - Visa total statistik i högerpanelen

2. **📈 Sentiment-analys**
   - Filtrera till endast positiva inlägg
   - Växla till värmekarta för att visa koncentration
   - Kommentera geografisk spridning

3. **⏰ Tidsresning**
   - Starta tidslinje-animation
   - Visa hur aktivitet växer över tid
   - Pausa vid intressanta datum/event

4. **🔍 Djupdykning**
   - Zooma in på Göteborg
   - Klicka på enskilda punkter för detaljer
   - Visa käll-fördelning i diagram

5. **🏗️ Teknik-demo**
   - Växla till 3D-vy för "wow-faktor"
   - Visa clustering-funktionalitet
   - Demonstrera sökning och filtrering

## 📋 **Checklista för lansering**

- [ ] ✅ GeoJSON-data laddas korrekt
- [ ] ✅ Alla fyra visualiseringslägen fungerar
- [ ] ✅ Tidslinje-animation är smooth
- [ ] ✅ Filter påverkar både karta och statistik
- [ ] ✅ Popups visar korrekt information
- [ ] ✅ Responsiv design fungerar på alla skärmar
- [ ] ✅ Performance är acceptabel (60fps)
- [ ] ✅ Export-funktionalitet fungerar
- [ ] ✅ Keyboard shortcuts fungerar
- [ ] ✅ No console errors

---

## 🎨 **Resultat**

Du har nu en **professionell datavisualisering** som skulle passa perfekt i Chalmers huvudbyggnad! Visualiseringen kombinerar:

- 🖤 **Modern mörk design** med neon-accenter
- 🗺️ **Avancerad kartfunktionalitet** med MapLibre GL JS
- ⚡ **Smooth 60fps animationer** och interaktioner
- 📊 **Omfattande statistik** och filtrering
- 📱 **Fullt responsiv** för alla enheter
- 🚀 **Enterprise-kvalitet** kod och performance

**Imponerande nog för att visa på Chalmers styrelserum! 🎉**