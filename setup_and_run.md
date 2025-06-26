# Chalmers Social Media Processor - Setup & Körning

## 📋 Förutsättningar

1. **Python 3.8+** installerat
2. **OpenAI API-nyckel** (från https://platform.openai.com/api-keys)
3. CSV-filen `Chalmers_SoMe - Jun 25, 2025 - 9 14 56 AM.csv` i Downloads-mappen

## 🚀 Installation

### 1. Installera beroenden
```bash
pip install -r requirements.txt
```

### 2. Sätt OpenAI API-nyckel
```bash
# macOS/Linux
export OPENAI_API_KEY='din-openai-api-nyckel-här'

# Windows
set OPENAI_API_KEY=din-openai-api-nyckel-här
```

## ▶️ Körning

### Kör scriptet
```bash
python chalmers_social_media_processor.py
```

## 📊 Vad scriptet gör

### 1. **CSV-läsning** 
- Läser UTF-16 LE kodad fil
- Kombinerar Datum + Tid till datetime

### 2. **Geocoding** (prioritetsordning)
- ✅ Stad → koordinater för staden
- ✅ Län → koordinater för länet  
- ✅ Region → koordinater för regionen
- ✅ Land → koordinater för landet
- ❌ Ingen geo-data → filtrerar bort

### 3. **LLM-filtrering** (OpenAI GPT-3.5)
- Analyserar brödtext för Chalmers-relevans
- Genererar rubrik (max 80 tecken)
- Skapar 3 nyckelord
- Bedömer sentiment (positiv/negativ/neutral)
- ❌ Inte relevant → filtrerar bort

### 4. **GeoJSON-export**
- Platt struktur (inga nestlade objekt)
- Kompatibel med MapLibre
- Sparas som `chalmers_social_media_maplibre.geojson`

## 📁 Output-fil struktur

```json
{
  "type": "FeatureCollection",
  "features": [
    {
      "type": "Feature", 
      "geometry": {
        "type": "Point",
        "coordinates": [11.9746, 57.6879]
      },
      "properties": {
        "id": "1750833037000_cUudZ9XGixUnwGIz0afQ-y407rIA",
        "datetime": "2025-06-25T08:30:00",
        "source": "Twitter",
        "sourceType": "social network",
        "account": "@oxhak", 
        "title": "Chalmers utvecklar kvantförstärkare",
        "originalText": "Researchers at Chalmers...",
        "url": "https://twitter.com/oxhak/statuses/...",
        "keywords": ["kvantdator", "energieffektiv", "förstärkare"],
        "sentiment": "positiv",
        "reach": 399,
        "ave": 3.69,
        "location": "Göteborg",
        "locationType": "stad"
      }
    }
  ]
}
```

## 🛠️ Funktioner

- **✅ Caching**: Geocoding och LLM-resultat cachas för snabbare körningar
- **✅ Progress bar**: Visar framsteg under bearbetning
- **✅ Logging**: Detaljerad loggning till fil och konsol
- **✅ Felhantering**: Robust hantering av API-fel och datafel
- **✅ Validering**: Kontrollerar GeoJSON-struktur innan export

## 📈 Förväntat resultat

- **Input**: ~1000+ rader social media-data
- **Output**: ~50-200 relevanta datapunkter (beroende på Chalmers-relevans)
- **Tid**: 5-15 minuter (beroende på antal LLM-anrop)

## 🚨 Felsökning

### Problem: "OPENAI_API_KEY inte satt"
**Lösning**: Sätt miljövariabeln enligt instruktioner ovan

### Problem: "CSV-fil hittades inte" 
**Lösning**: Kontrollera att filen finns i Downloads-mappen

### Problem: "Rate limit exceeded"
**Lösning**: Scriptet pausar automatiskt mellan API-anrop

### Problem: "Få/inga resultat"
**Lösning**: Kontrollera att brödtexten verkligen nämner Chalmers

## 📊 Optimeringar

- **Geocoding**: Använder lokal databas för svenska platser (snabbare)
- **LLM**: Cachar resultat för identiska texter  
- **Rate limiting**: Automatisk väntan mellan API-anrop
- **Batch processing**: Effektiv bearbetning av stora dataset

## 🔄 Exempel på körning

```bash
$ python chalmers_social_media_processor.py

2025-06-25 10:30:00 - INFO - === CHALMERS SOCIAL MEDIA PROCESSOR ===
2025-06-25 10:30:01 - INFO - Läser CSV-fil: /Users/.../Chalmers_SoMe...csv
2025-06-25 10:30:02 - INFO - Läste 1250 rader med 42 kolumner
2025-06-25 10:30:02 - INFO - Kombinerar datum och tid
2025-06-25 10:30:03 - INFO - Börjar bearbeta data...
Bearbetar data: 100%|████████| 1250/1250 [08:32<00:00,  2.4it/s]
2025-06-25 10:38:35 - INFO - Bearbetning klar. 87 datapunkter behållna, 1163 filtrerade bort
2025-06-25 10:38:35 - INFO - GeoJSON skapad med 87 features
2025-06-25 10:38:35 - INFO - GeoJSON-validering lyckades
2025-06-25 10:38:35 - INFO - GeoJSON sparad till chalmers_social_media_maplibre.geojson
2025-06-25 10:38:35 - INFO - === SLUTSTATISTIK ===
2025-06-25 10:38:35 - INFO - Input-rader: 1250
2025-06-25 10:38:35 - INFO - Output-features: 87
2025-06-25 10:38:35 - INFO - Success rate: 7.0%
2025-06-25 10:38:35 - INFO - Sentiment-fördelning: {'positiv': 65, 'neutral': 18, 'negativ': 4}
2025-06-25 10:38:35 - INFO - Platstyp-fördelning: {'stad': 45, 'land': 32, 'län': 8, 'region': 2}

✅ Bearbetning klar! GeoJSON sparad som: chalmers_social_media_maplibre.geojson
```

## 📋 Nästa steg

1. **Kör scriptet** enligt instruktioner ovan
2. **Importera GeoJSON** i MapLibre
3. **Konfigurera visualisering** baserat på properties (sentiment, locationType, etc.)
4. **Anpassa styling** för olika datapunktstyper

---

**Skapad av**: Thea Törnqvist  
**Datum**: 2025-06-25