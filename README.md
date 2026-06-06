# HTML Forge 🔥

**Local framework that generates HTML pages from natural language prompts**, powered by [Ollama](https://ollama.com).  
New: **Screenshot → HTML** (vision models) and **localStorage persistence**.

---

## Quick start with Docker Compose

```bash
# 1. Enter the project folder
cd ollama-html-forge

# 2. (Optional) pick your models in .env
#    Defaults: qwen2.5:7b (text) + llama3.2-vision:11b (vision)

# 3. Start everything
docker compose up -d

# First boot downloads both models automatically (~4–8 GB).
# Watch progress with:
docker compose logs -f model-puller
```

Open **http://localhost:8080** in your browser.

> **NVIDIA GPU**: uncomment the `deploy` block in `docker-compose.yml`.

---

## Manual start (no Docker)

### 1. Install Ollama

```bash
# macOS / Linux
curl -fsSL https://ollama.com/install.sh | sh
```

### 2. Pull models

```bash
# Text model (required)
ollama pull qwen2.5:7b

# Vision model (for Screenshot → HTML)
ollama pull llama3.2-vision:11b   # recommended
# ollama pull llava:13b
# ollama pull gemma3:12b
```

### 3. Open the UI

Open `index.html` directly in your browser, or serve it:

```bash
python3 -m http.server 8000
# then visit http://localhost:8000
```

---

## Features

| Feature | Description |
|---|---|
| **Generate** | Create an HTML page from a text prompt |
| **Screenshot → HTML** | Upload/paste/drop a mockup image; a vision model recreates it as HTML |
| **Refine** | Iterate on the current page with follow-up instructions (multi-turn) |
| **6 Visual styles** | Modern · Minimal · Retro/80s · Glass · Brutalist · Dark luxury |
| **8 Quick templates** | Landing · Portfolio · Dashboard · Blog · Form · Product · Pricing · 404 |
| **Live preview** | Rendered page in an iframe |
| **Code view** | Editable HTML source |
| **Copy / .html / .zip** | Export the page (ZIP splits CSS + JS into separate files) |
| **Persistent history** | Up to 30 generations saved in localStorage — survives page refresh |
| **Persistent settings** | URL, temperature, tokens, system prompt — all saved automatically |
| **Streaming** | Tokens arrive in real-time |
| **Auto proxy detection** | Detects Nginx proxy (Docker) or direct Ollama automatically |
| **Paste from clipboard** | Paste a screenshot with Ctrl+V anywhere on the page |

---

## Keyboard shortcuts

| Key | Action |
|---|---|
| `Ctrl+Enter` | Smart dispatch: From Image (if image loaded) → Refine (if refine text) → Generate |
| `Ctrl+V` | Paste an image from clipboard directly |

---

## Project structure

```
ollama-html-forge/
├── docker-compose.yml   # Orchestrates Ollama + Nginx
├── .env                 # Model names, UI port
├── nginx/
│   └── default.conf     # Frontend + /ollama/ reverse proxy
├── index.html           # Entire application (single file)
└── README.md
```

---

## Docker commands

```bash
docker compose down                  # Stop
docker compose logs -f               # Live logs
docker compose down -v               # Stop + delete model volumes
docker compose pull && docker compose up -d   # Update images
```

---

## Recommended models

| Model | Type | RAM | Notes |
|---|---|---|---|
| `qwen2.5:7b` | Text | ~5 GB | ⭐ Default, great for HTML/CSS |
| `llama3.2:3b` | Text | ~2 GB | Lightweight, low-RAM machines |
| `codellama:13b` | Text | ~8 GB | Code-specialised |
| `llama3.2-vision:11b` | Vision | ~8 GB | ⭐ Best for screenshot→HTML |
| `llava:13b` | Vision | ~8 GB | Alternative vision model |
| `gemma3:12b` | Vision | ~8 GB | Google vision model |
| `minicpm-v:8b` | Vision | ~6 GB | Lightweight vision option |

---

Made with ❤ + Ollama
