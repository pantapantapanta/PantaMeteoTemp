# Meteo — La Terrazza

**Turin Palace Hotel · Torino**

Previsioni meteo e valutazione condizioni per la terrazza del Turin Palace Hotel.

## Deploy

Il sito è deployato su [Render](https://render.com) con auto-deploy dal branch `main`.

```bash
npm install
npm start
```

Il server gira sulla porta definita dalla variabile d'ambiente `PORT` (default: 3000).

## Struttura

```
├── server.js          # Express server
├── package.json       # Dipendenze
├── render.yaml        # Config Render
├── public/
│   ├── index.html     # App principale
│   ├── manifest.json  # PWA manifest
│   ├── icon-turin-palace-meteo.svg
│   ├── icon-turin-palace-meteo-512.png
│   └── apple-touch-icon.png
└── PROPOSTA-TURIN-PALACE-METEO.md
```

## Tecnologia

Powered by [PantaMeteo](https://github.com/pantapantapanta/PantaMeteo) · 13 modelli · Calibrazione ERA5
