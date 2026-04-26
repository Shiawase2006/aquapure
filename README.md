# AquaPure 💧
### Intelligent Water Quality Assessment System

A standalone, browser-based decision support system that assesses drinking water quality and recommends suitable **chlorine-free purification methods** based on pH, turbidity, and TDS parameters. Includes an AI-powered water quality advisor, trend analytics, and 27 global river/source presets.

---

---

## 📸 Features

| Feature | Description |
|---|---|
| 🔬 Water Quality Assessment | Weighted scoring across pH, turbidity, and TDS parameters |
| 💡 Purification Recommendations | Chlorine-free methods: SODIS, UV, RO, boiling, activated carbon, combination systems |
| 🌊 River & Source Presets | 27 global presets across Asia, Europe, Americas, Africa, and common source types |
| 🤖 AI Water Advisor | Claude API-powered plain-language interpretation of results |
| 📈 Trend Sparklines | Visual bar chart history across your last 10 records |
| 🔮 Predictive Analytics | Linear regression forecast of next water quality category |
| 📤 CSV Export | One-click export of all saved assessment records |
| 💾 Persistent History | Up to 20 records stored locally via `localStorage` |
| 📱 Responsive Design | Mobile-friendly layout with working hamburger nav |

---

## 🧪 How the Assessment Works

AquaPure uses a **weighted scoring model** across three primary water quality parameters:

| Parameter | Weight | Safe Range | Standard |
|---|---|---|---|
| pH | 40% | 6.5 – 8.5 | WHO / BIS |
| TDS | 30% | < 500 mg/L | WHO / BIS |
| Turbidity | 30% | < 5 NTU | WHO / BIS |

### Scoring Logic

Each parameter is scored 0–100 using piecewise linear interpolation:

- **pH**: Full score at ideal (7.2), degraded linearly toward boundaries (6.5 / 8.5), zero near extremes
- **Turbidity**: Full score ≤ 1 NTU, degraded 1–5 NTU, critical above 5 NTU
- **TDS**: Full score ≤ 300 mg/L, graduated penalty to 1000 mg/L, critical above 1000 mg/L

The **overall quality score** is a weighted average of all three component scores.

### Safety Categories

| Score Range | Category | Treatment |
|---|---|---|
| 90 – 100 | Excellent | Not required |
| 75 – 89 | Good | Recommended |
| 60 – 74 | Moderate | Required |
| 40 – 59 | Poor | Immediate |
| 0 – 39 | Critical | Multiple methods |

---

## 🌊 River & Source Presets

Reference values drawn from published water quality monitoring reports (WHO, CPCB, USEPA, peer-reviewed studies). These are **typical reference ranges**, not live sensor readings.

### Asia
Ganga (Varanasi), Yamuna (Delhi), Brahmaputra, Godavari, Krishna, Indus, Cauvery, Mekong, Yangtze, Ganges Delta

### Europe
Thames, Rhine, Danube, Seine, Elbe, Volga

### Americas
Mississippi, Amazon, Colorado, Rio Grande, Orinoco, St. Lawrence

### Africa & Others
Nile, Congo, Niger, Zambezi, Orange River

### Source Types
Municipal Tap, Deep Borewell, Shallow Well, Rainwater, Mountain Spring, Village Pond

---

## 💧 Purification Methods Covered

1. **SODIS (Solar Disinfection)** — UV radiation in PET bottles, 6–48 hours
2. **Activated Carbon Filtration** — Removes chemicals, odours, and taste issues
3. **Reverse Osmosis** — Membrane filtration, 95–99% contaminant removal
4. **Boiling** — 100°C for 1–3 minutes, eliminates all pathogens
5. **UV Radiation** — Instant disinfection without chemicals
6. **Combination Systems** — Multi-stage treatment for severe contamination

Each method card includes step-by-step instructions and a list of contaminants it is effective against.

---

## 🤖 AI Water Advisor

The AI advisor uses the **Anthropic Claude API** (`claude-sonnet-4-20250514`) to generate a plain-language interpretation of your results. It covers:

- What the results mean in everyday terms
- The most concerning parameter and why
- Which purification method to prioritise and how to implement it
- Seasonal or regional considerations based on source type

> **Note:** The AI advisor requires a network connection and is rate-limited by the Anthropic API. No API key is required from the user — the integration uses the platform's built-in credentials when deployed via Claude Artifacts.

---

## 📊 Predictive Analytics

AquaPure uses **simple linear regression** on the last 2–6 saved records (filtered by dataset tag) to forecast the next expected water quality category and parameter values.

- Confidence level: Low (2 records), Medium (3), High (4+)
- Predictions are tag-filtered so you can track specific sites or sources separately
- The model updates automatically each time a new record is saved

> This is a lightweight trend indicator, not a statistically rigorous forecast. For research applications, integration with a proper time-series model (e.g. ARIMA or ML-based) is recommended.

---

## 🛠 Technology Stack

| Technology | Purpose |
|---|---|
| HTML5 | Single-file page structure |
| Tailwind CSS (CDN) | Responsive utility-first styling |
| Vanilla JavaScript | Assessment logic, UI rendering, analytics |
| localStorage | Persistent record history (up to 20 entries) |
| Anthropic Claude API | AI-powered water quality advisor |
| Font Awesome (CDN) | Icons |

No build tools, no dependencies to install, no backend required.

---

## 📁 Project Structure

```
aquapure/
├── index.html        # Entire application (single file)
└── README.md         # This file
```

---

## 📋 Water Quality Standards Referenced

- **WHO** — Guidelines for Drinking-water Quality (4th edition)
- **BIS IS 10500:2012** — Indian Standard for Drinking Water
- **USEPA** — National Primary and Secondary Drinking Water Regulations
- **CPCB** — Central Pollution Control Board river monitoring data (India)

---

## 🔮 Potential Improvements

- [ ] Connect to live IoT sensor data via MQTT or REST API
- [ ] Add CPCB / USGS real-time river quality API integration
- [ ] Replace linear regression with ARIMA or ML-based forecasting
- [ ] Add user authentication and cloud-based record sync
- [ ] Multi-language support (Hindi, Tamil, Bengali, etc.)
- [ ] Offline PWA support with service workers
- [ ] Add bacteriological parameters (E. coli, coliform count)
- [ ] Printable PDF assessment report

---

## 📄 License

This project is open source and available under the [MIT License](LICENSE).

---

## 👤 Author

Built as a software-based decision system for assessing drinking water quality and recommending chlorine-free purification methods.

> *Reference parameter values are sourced from WHO, BIS, USEPA, and published peer-reviewed water quality studies. This tool is intended for educational and decision-support purposes and does not replace laboratory water testing.*
