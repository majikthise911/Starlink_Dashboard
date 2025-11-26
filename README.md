# Starlink Link Budget Calculator

An interactive web tool that calculates how altitude affects Starlink satellite internet signal strength. Search any location, get its elevation, and see real-time link budget comparisons.

![Dashboard Preview](preview.png)

## 🚀 Live Demo

[Try the calculator →](https://your-deployed-url.netlify.app)

## What It Does

Ever wonder why satellite internet might work better on a mountain than at the beach? This calculator shows you exactly why — with real physics.

**Key Features:**
- 🔍 Search any location worldwide
- 🏔️ Auto-fetches elevation data
- 📊 Calculates water vapor reduction at altitude
- 📡 Compares path loss vs. sea level across weather conditions
- 💡 Plain-English explanations for non-engineers

## The Science (TL;DR)

Starlink uses Ku-band frequencies (~12 GHz) which are absorbed by water vapor in the atmosphere. Water vapor density decreases exponentially with altitude (scale height ≈ 2 km). 

**At 4,300m (14,000 ft), you're above ~88% of atmospheric water vapor.**

This means:
- Less signal absorption
- No cloud attenuation (you're above them)
- No rain fade (rain falls below you)
- **Up to 6-20 dB better link margin in bad weather**

That 6 dB? It's 4× the received power. The difference between "connection lost" and "streaming 4K."

## Quick Start

### Option 1: Just Open It
Download `starlink_calculator.html` and open it in any browser. That's it — it's fully self-contained.

### Option 2: Deploy It
Drag the HTML file to [Netlify Drop](https://app.netlify.com/drop) for an instant public URL.

### Option 3: GitHub Pages
1. Create a new repository
2. Upload `starlink_calculator.html` as `index.html`
3. Enable GitHub Pages in Settings
4. Access at `yourusername.github.io/repo-name`

## Technical Details

### Link Budget Parameters

| Parameter | Value | Source |
|-----------|-------|--------|
| Frequency Band | Ku-band (10.7-12.7 GHz) | FCC Filing |
| Center Frequency | 12 GHz | — |
| Orbital Altitude | 550 km | SpaceX Spec |
| Free Space Path Loss | ~176 dB @ 25° elevation | Calculated |
| Water Vapor Scale Height | 2 km | ITU-R P.676 |

### Atmospheric Loss Model

```
Water Vapor Factor = e^(-altitude / 2000m)
Cloud Factor = max(0, 1 - altitude / 3000m)  
Rain Factor = max(0, 1 - altitude / 2500m)
```

### Weather Scenarios

| Condition | Sea Level Losses | At 4,300m | Advantage |
|-----------|-----------------|-----------|-----------|
| Clear Sky | 0.2 dB | 0.02 dB | +0.2 dB |
| Partly Cloudy | 1.35 dB | 0.04 dB | +1.3 dB |
| Rainy | 6.0 dB | 0.06 dB | +5.9 dB |
| Heavy Storm | 15.6 dB | 0.07 dB | +15.5 dB |

## APIs Used

- **[Nominatim](https://nominatim.org/)** — Location geocoding (OpenStreetMap)
- **[Open-Elevation](https://open-elevation.com/)** — Elevation data
- **[Leaflet](https://leafletjs.com/)** — Interactive maps
- **[CARTO](https://carto.com/)** — Dark map tiles

All APIs are free and require no API keys.

## Browser Compatibility

Works in all modern browsers:
- Chrome, Firefox, Safari, Edge
- Mobile browsers (responsive design)

## Project Context

Built as part of **SPCE 5400 — Small Satellite Engineering & Operations** coursework, inspired by testing a Starlink Mini at 14,000 ft in the Andes mountains near Mendoza, Argentina.

The connection didn't just work — it thrived. This tool explains why.

## Files

```
├── starlink_calculator.html   # Interactive calculator (main file)
├── starlink_dashboard.html    # Static version (Mendoza only)
├── starlink_link_budget.md    # Detailed analysis document
└── README.md                  # This file
```

## License

MIT — Use it however you want.

## Author

**Jordan Clayton**  
Masters in Engineering — Space Operations  
November 2025

---

*"Your office is now anywhere you dare to take it. Even the places HR would prefer you didn't."*
