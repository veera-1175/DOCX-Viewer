# DOCX-Viewer

### Lightweight in-browser Word document viewer (Office Online embed)

[![HTML5](https://img.shields.io/badge/HTML5-E34F26?logo=html5&logoColor=white)](https://developer.mozilla.org/en-US/docs/Web/HTML)
[![CSS3](https://img.shields.io/badge/CSS3-1572B6?logo=css3&logoColor=white)](https://developer.mozilla.org/en-US/docs/Web/CSS)
[![License](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

> Open `.docx` files in the browser with one click — no desktop Word, no upload-to-random-site friction. Built around Microsoft’s Office Online embed viewer.

Solo-built by **[Veerasegaran V P](https://github.com/veera-1175)** as a focused front-end utility: clean UI, zero backend, instant previews.

---

## Why this exists

Teams and creators often need to **preview Word docs in a browser** (handouts, specs, shared notes) without forcing downloads or installing Office. This project wraps the Office Online embed endpoint in a minimal, responsive shell:

- Pick a document → iframe loads `view.officeapps.live.com`
- Works with any publicly reachable `.docx` URL (static hosting / CDN)
- No auth server, no database — drop files under `docs/` and ship

---

## Features

- One-click document switcher
- Full-width embed viewer
- Static site — host on GitHub Pages, Netlify, nginx, or any file server
- Sample docs included under `docs/` (swap in your own)

---

## Quick start

Serve the folder over **HTTP(S)** (Office Online needs a real URL, not `file://`):

```powershell
git clone https://github.com/veera-1175/DOCX-Viewer.git
cd DOCX-Viewer

# Python
python -m http.server 5500

# Or VS Code Live Server / any static host
```

Open `http://localhost:5500` → click a document button.

### Add your own files

1. Drop `.docx` files into `docs/`
2. Add a button in `index.html`:

```html
<button onclick="openDoc('docs/your-file.docx')">Your label</button>
```

---

## How it works

```javascript
function openDoc(file) {
  const url = window.location.origin + "/" + file;
  document.getElementById("viewer").src =
    "https://view.officeapps.live.com/op/embed.aspx?src=" +
    encodeURIComponent(url);
}
```

| Constraint | Implication |
|------------|-------------|
| Document URL must be publicly reachable | Localhost embeds only work if Microsoft can fetch that URL — for real demos, deploy static hosting |
| CORS / hosting | Serve over HTTP; keep `.docx` on the same origin path |
| No server logic | Pure static HTML/CSS/JS |

---

## Project structure

```
DOCX-Viewer/
├── index.html      # Switcher + iframe
├── style.css       # Layout / theme
├── docs/           # Sample .docx files
└── README.md
```

---

## Interview walkthrough

| Topic | Talking point |
|-------|----------------|
| Scope discipline | Small utility done well — not a bloated CMS |
| Integration skill | Leveraging Office Online embed correctly |
| UX | Clear CTAs, dedicated viewer pane, responsive shell |
| Deploy awareness | Static hosting + public URL constraints |

---

## License

MIT © [Veerasegaran V P](https://github.com/veera-1175)

**DOCX-Viewer** — Word previews without the install.
