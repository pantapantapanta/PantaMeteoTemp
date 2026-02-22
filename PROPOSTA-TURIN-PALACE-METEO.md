# Proposta: PantaMeteo → Meteo — La Terrazza

**Per**: Turin Palace Hotel
**Da**: Leo (Bocconi) — Febbraio 2026
**Repo**: `pantapantapanta/PantaMeteoTurinPalace`
**Deploy**: Render (auto-deploy da branch `main`)

---

## 1. Analisi dello stile Turin Palace Hotel

Dall'analisi di [turinpalacehotel.com](https://www.turinpalacehotel.com/):

| Elemento | Valore estratto |
|----------|----------------|
| Colore primario | `#5B7186` (blu ardesia) |
| Testo body | `#777777` |
| Testo scuro | `#222222` |
| Footer background | `#5B7186` |
| Font headline | ChampagneLimo |
| Font body | Amiri (serif) |
| Font UI | Quattrocento Sans |
| Design language | Lusso europeo classico, whitespace, tipografia serif |

---

## 2. Palette colori proposta

| Funzione | PantaMeteo attuale | Turin Palace proposto |
|----------|-------------------|----------------------|
| Primario | `#2196F3` (blu elettrico) | `#5B7186` (blu ardesia) |
| Sfondo | `#1a1a2e` (scuro) | `#FAFAF8` (avorio caldo) |
| Sfondo card | `#16213e` | `#FFFFFF` |
| Accento positivo | `#4CAF50` (verde) | `#8B9E6B` (verde salvia) |
| Accento caldo | `#FF9800` (arancio) | `#C4A35A` (oro antico) |
| Accento negativo | `#f44336` (rosso) | `#A0522D` (rosso mattone) |
| Testo primario | `#FFFFFF` | `#222222` |
| Testo secondario | `rgba(255,255,255,0.7)` | `#777777` |
| Dark mode sfondo | invariato | `#2C3E4A` |
| Dark mode card | invariato | `#354B5A` |

---

## 3. Tipografia proposta

| Ruolo | Attuale | Proposto | Fallback |
|-------|---------|----------|----------|
| Display / titoli | system sans-serif | Playfair Display | Georgia, serif |
| Body / dati | system sans-serif | Inter | system-ui, sans-serif |
| Monospace (dati) | invariato | JetBrains Mono | monospace |

Caricamento via Google Fonts:
```html
<link href="https://fonts.googleapis.com/css2?family=Playfair+Display:ital,wght@0,400;0,700;1,400&family=Inter:wght@300;400;500;600&display=swap" rel="stylesheet">
```

---

## 4. Modifiche funzionali

### 4.1 Single-city mode
- Rimuovere ricerca città e preferiti
- Bloccare su **Torino** come unica località
- Header semplificato: logo + nome + toggle dark mode

### 4.2 Terrazza come Hero Section
Attualmente la Terrazza è una feature secondaria (toggle nel footer). Proposta: **elevarla a sezione hero** subito sotto l'header.

Componenti della card Hero Terrazza:
- **Score circolare** (0–100) con colore dinamico
- **Verdetto testuale**: "Serata ideale", "Condizioni buone", "Sconsigliato", "Non disponibile"
- **Metriche chiave**: temperatura, vento, precipitazione, con icone e barre di progresso
- **Fascia oraria**: configurabile (default 19:00–23:00)

### 4.3 Stazione WU — La Terrazza Live
- Stazione `ITURIN3276` già configurata in `server.js`
- Rinominare label da "Stazione WU" a **"La Terrazza — Live"**
- Dati real-time: temperatura, umidità, vento, pressione

### 4.4 Linguaggio hospitality
Sostituire il linguaggio tecnico-meteorologico con toni adatti all'ospitalità:

| Attuale | Proposto |
|---------|----------|
| "Consensus dei modelli" | "Le previsioni concordano" |
| "Skill score" | rimuovere o spostare in sezione avanzata |
| "Precipitazione mm/h" | "Possibilità di pioggia" |
| "CAPE J/kg" | rimuovere |

### 4.5 Semplificazione interfaccia
- Rimuovere: tabella comparativa modelli (o renderla collassabile "Per esperti")
- Rimuovere: indici tecnici (CAPE, CIN, lifted index)
- Mantenere: previsione 8 giorni, grafici temperatura/vento/precipitazione, alba/tramonto

---

## 5. Modifiche server

Il `server.js` richiede modifiche minime:

1. **Endpoint `/api/stations`**: restituire solo Torino
2. **Label WU**: aggiungere campo `label: "La Terrazza — Live"` nella config stazione
3. **Nessuna modifica** agli endpoint proxy WU, METAR, modelli

---

## 6. Struttura file proposta

```
PantaMeteoTurinPalace/
├── index.html                          # SPA principale (modificata)
├── server.js                           # Server Node.js (modifiche minime)
├── package.json                        # Dipendenze
├── render.yaml                         # Config Render deploy
├── icon-turin-palace-meteo.svg         # Icona vettoriale
├── icon-turin-palace-meteo-512.png     # Icona PWA 512×512
├── apple-touch-icon-terrazza.png       # Icona iOS 180×180
├── mockup-turin-palace-meteo.html      # Mockup interattivo (reference)
├── PROPOSTA-TURIN-PALACE-METEO.md      # Questo documento
├── metodologia.md                      # Metodologia PantaMeteo (invariata)
└── README.md                           # Da aggiornare
```

---

## 7. Cosa NON cambia

- **Motore previsionale**: 13 modelli con calibrazione skill-based vs ERA5
- **Logica Terrazza**: `evalTerrazza()` con scoring multi-parametro
- **Proxy WU/METAR**: endpoint e logica di fallback
- **Dark mode**: mantenuto, adattato alla nuova palette
- **Responsive**: mantenuto
- **PWA**: mantenuto, aggiornato manifest con nuove icone

---

## 8. Roadmap implementazione

| Fase | Attività | Effort stimato |
|------|----------|---------------|
| 1 | Rebranding CSS (palette, font, variabili) | 4h |
| 2 | Hero Terrazza (layout, score, verdetto) | 6h |
| 3 | Single-city mode + semplificazione UI | 3h |
| 4 | Linguaggio hospitality + label WU | 2h |
| 5 | Icone PWA + manifest | 1h |
| 6 | Test responsivo + dark mode | 2h |
| 7 | Deploy su Render + test finale | 1h |
| **Totale** | | **~19h** |
