# API-Integration

API INTEGRATION

Company Name: CODTECH IT SOLUTIONS

Name: Rajratna Nitin Kamble

Intern ID: CTIS3288

Domain Name: Full Stack Web Development

Batch Duration: 8 Weeks

Mentor Name: Nila Santos

# NEXUS — Ultimate Entertainment Hub

> A single-file, zero-dependency web application that aggregates seven live data sources into one dark-themed dashboard — news, weather, anime, music, trivia, space launches, and comics.

---

## 📸 Overview

NEXUS is a pure HTML/CSS/JavaScript entertainment dashboard. There is no build step, no framework, no package manager. Drop the file in a browser and it works.

---

## ✨ Features

| Panel | Source | What it shows |
|---|---|---|
| 🌐 **News** | The Guardian API | Latest headlines with featured story + article list |
| 🌤️ **Weather** | Open-Meteo + Geocoding API | Real-time conditions for any city worldwide |
| 🎌 **Anime** | Jikan v4 (MyAnimeList) | Trending, Top Rated & Upcoming anime |
| 🎵 **Music** | MusicBrainz API | Search recordings by artist or song title |
| 🎯 **Trivia** | Open Trivia DB | Random multiple-choice questions across categories |
| 🚀 **Space** | SpaceX v4 API | Recent and upcoming SpaceX launch events |
| 📚 **Comics** | Curated local database | 32 iconic characters with first appearance info |

---

## 🚀 Getting Started

### Prerequisites

None. This is a standalone HTML file. You only need a modern web browser (Chrome, Firefox, Safari, Edge).

### Running Locally

```bash
# Clone or download the file, then simply open it:
open nexus.html

# Or serve it with any static server, e.g. Python:
python -m http.server 8000
# Then visit: http://localhost:8000/nexus.html
```

### Deploying

Since it's a single file, you can host it anywhere static files are served:

- **GitHub Pages** — push to a repo, enable Pages in settings
- **Netlify / Vercel** — drag and drop the file into the dashboard
- **Any web host** — upload via FTP

---

## 🗂️ Project Structure

```
nexus.html
│
├── <style>          CSS — reset, layout, theming, all panel styles,
│                    responsive breakpoints (768px, 480px)
│
├── <body>           HTML — topbar nav, hero section, 7 content panels
│
└── <script>         JavaScript — panel router, 7 async data fetchers,
                     trivia logic, comics search filter
```

Everything lives in one file. No external JS files, no CSS files, no config.

---

## 🌐 APIs Used

All APIs are **free** and require **no authentication** unless noted.

### 1. The Guardian
- **Endpoint:** `https://content.guardianapis.com/search`
- **Key required:** Uses the public `test` key (rate-limited but functional)
- **Docs:** [open-platform.theguardian.com](https://open-platform.theguardian.com/)

### 2. Open-Meteo
- **Endpoints:**
  - Geocoding: `https://geocoding-api.open-meteo.com/v1/search`
  - Forecast: `https://api.open-meteo.com/v1/forecast`
- **Key required:** No
- **Docs:** [open-meteo.com/en/docs](https://open-meteo.com/en/docs)

### 3. Jikan v4
- **Endpoint:** `https://api.jikan.moe/v4/top/anime`
- **Key required:** No (unofficial MAL wrapper)
- **Rate limit:** 3 requests/second, 60/minute
- **Docs:** [docs.api.jikan.moe](https://docs.api.jikan.moe/)

### 4. MusicBrainz
- **Endpoint:** `https://musicbrainz.org/ws/2/recording`
- **Key required:** No
- **Note:** Requires a `User-Agent` header (already set in the code)
- **Docs:** [musicbrainz.org/doc/MusicBrainz_API](https://musicbrainz.org/doc/MusicBrainz_API)

### 5. Open Trivia DB
- **Endpoint:** `https://opentdb.com/api.php`
- **Key required:** No
- **Encoding:** Uses `url3986` to avoid HTML entity issues
- **Docs:** [opentdb.com/api_config.php](https://opentdb.com/api_config.php)

### 6. SpaceX v4
- **Endpoint:** `https://api.spacexdata.com/v4/launches/query` (POST)
- **Key required:** No
- **Docs:** [github.com/r-spacex/SpaceX-API](https://github.com/r-spacex/SpaceX-API)

### 7. Comics (Local)
- **Source:** Curated static dataset — 32 characters across Marvel & DC
- **Key required:** N/A
- **Note:** Replaced ComicVine (requires paid key + server-side proxy due to CORS)

---

## 🏗️ Architecture

### Panel Router

Navigation is handled by a simple client-side router. Each nav button calls `go(id, btn)` which toggles the `active` class on panels and tracks which panels have already been loaded to avoid redundant API calls.

```js
function go(id, btn) {
    // hide all panels, deactivate all nav buttons
    // show target panel, mark button active
    // fetch data only if panel hasn't been loaded yet
}
```

### Data Fetching Pattern

Every fetcher follows the same pattern:

1. Show a loading spinner
2. `await fetch(url)`
3. Render HTML from the response data
4. Catch errors and show a styled error box

### Trivia Answer Safety

Trivia options are stored in `data-value` attributes on buttons rather than embedded in `onclick` strings. This prevents breakage when answers contain apostrophes, quotes, or special characters.

---

## 🎨 Design System

### Fonts
- **Display:** Bebas Neue (headings, numbers, logo)
- **Body:** Outfit 300–700 (all UI text)
- Both loaded from Google Fonts

### Color Palette

| Token | Hex | Usage |
|---|---|---|
| Background | `#07070b` | Page background |
| Surface | `#0f0f16` | Cards |
| Surface 2 | `#16161f` | Inputs, hover states |
| Border | `#2a2a3a` | All dividers and borders |
| Text primary | `#eae8e0` | Headings and body |
| Text muted | `#7a7a8a` | Subtitles, descriptions |
| Text faint | `#4a4a55` | Labels, metadata |
| Gold | `#e8c44a` | Primary accent (active states, scores) |
| Pink | `#ff5e7a` | Anime tabs, error states |
| Teal | `#3dd9c0` | Music accent |
| Orange | `#ff8c42` | Comics accent |
| Blue | `#4fa3e8` | Space dates, upcoming badges |
| Purple | `#9b6dff` | Trivia category, quote tags |
| Green | `#52e08a` | Correct trivia answer |

### Responsive Breakpoints

```
> 768px   — Full desktop layout (4-column grids, 2-column news)
≤ 768px   — Tablet (3-column grids, stacked nav, single-column news)
≤ 480px   — Mobile (2-column grids, tighter padding throughout)
```

---

## ⚙️ Customisation

### Change the default city (Weather)
Edit the `value` attribute on the city input:
```html
<input ... value="London" ...>
```

### Change the default music search
Edit the `value` attribute on the music input:
```html
<input ... value="Coldplay" ...>
```

### Add more comics characters
Extend the `COMICS_DB` array in the script:
```js
{ name:'Nightwing', first:'Tales of the Teen Titans #44', year:'1984', publisher:'DC', emoji:'🦅' },
```

### Swap to a real Guardian API key
Replace `api-key=test` in `fetchNews()` with your key from [open-platform.theguardian.com](https://open-platform.theguardian.com/). The `test` key works but is rate-limited and returns the same articles frequently.

---

## 🐛 Known Limitations

- **The Guardian `test` key** is rate-limited and may occasionally return cached or repeated articles. Register for a free developer key for better results.
- **Jikan API** enforces a rate limit of 60 requests/minute. Rapid tab switching may temporarily return errors.
- **MusicBrainz** can be slow on the first query due to their search index. Subsequent searches are faster.
- **SpaceX API** only covers SpaceX missions. For all-agency launches, consider [Launch Library 2](https://ll.thespacedevs.com/2.2.0/).
- **Comics panel** uses a local static dataset. It does not fetch live data and is limited to the 32 pre-defined characters.

---

## 📄 License

This project is released for personal and educational use. API usage is subject to each provider's own terms of service.

---

## 🙏 Acknowledgements

- [The Guardian Open Platform](https://open-platform.theguardian.com/)
- [Open-Meteo](https://open-meteo.com/)
- [Jikan — Unofficial MyAnimeList API](https://jikan.moe/)
- [MusicBrainz](https://musicbrainz.org/)
- [Open Trivia Database](https://opentdb.com/)
- [SpaceX API by r/SpaceX](https://github.com/r-spacex/SpaceX-API)
- Fonts by [Google Fonts](https://fonts.google.com/)
