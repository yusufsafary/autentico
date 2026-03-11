# ◆ Autentico

**AI-powered Folklore Generator** — Choose a country, pick a folklore type, and let AI bring ancient tales to life with narrative, original art, and atmospheric audio.

---

## Overview

Autentico is a web-based storytelling platform that generates culturally-authentic folklore from 80+ countries. Users select a region and story type, and the AI produces a full narrative experience combining written story, illustration, and voice narration.

**Live demo:** `autentico.html` (single-file prototype)

---

## Features

| Feature | Description |
|---|---|
| 🌍 **Country Selector** | 80+ countries across Asia, Europe, Africa, Americas, Middle East |
| 📖 **Folklore Types** | Origin Myth, Hero's Journey, Spirit Tale, Trickster, Love Legend, Epic Saga, and more |
| 🎨 **Art Generation** | Culturally-rooted illustration styles (Batik, Ukiyo-e, Ink & Brush, Watercolor, etc.) |
| 🎙️ **Audio Narration** | Atmospheric voice narration with traditional instruments |
| ⚙️ **Advanced Options** | Tone, output format, story length, art style — collapsible to keep UI clean |
| 📱 **Mobile-first** | Fully responsive, touch-optimised, hamburger nav on mobile |

---

## Pages

### 1. Landing Page
- Hero section with animated prompt generator
- Quick-select tags (Japan · Ghost Tale, Indonesia · Myth, etc.)
- How it works (3 steps)
- Example generated stories grid
- Region explorer (80+ cultures)
- Feature highlights
- CTA

### 2. Story Page (Mock)
- Full-bleed cinematic hero with floating orbs and batik pattern
- Sticky audio player with play/pause, progress bar, seek
- Two-column layout: narrative text + sidebar (metadata, share, cultural context)
- Drop cap, pull quotes, inline illustration breaks
- Related stories section

---

## Tech Stack (Current Prototype)

```
autentico.html        Single-file HTML/CSS/JS prototype
                      No dependencies, no build step
                      Fonts via Google Fonts CDN
```

### Planned Production Stack

```
Frontend              Next.js + Tailwind CSS
AI (Story)            Anthropic Claude API (claude-sonnet-4-6)
AI (Image)            Stable Diffusion / FLUX via Replicate or fal.ai
AI (Audio)            ElevenLabs or PlayHT for voice narration
Backend               Node.js + FastAPI (Python)
Database              PostgreSQL (stories) + Redis (cache)
Storage               Cloudflare R2 / S3 (images & audio)
Auth                  Clerk or Supabase Auth
Hosting               Vercel (frontend) + Railway (backend)
```

---

## Project Structure (Planned)

```
autentico/
├── frontend/
│   ├── pages/
│   │   ├── index.tsx          # Landing + prompt generator
│   │   ├── story/[id].tsx     # Story reader page
│   │   └── library.tsx        # Saved stories
│   ├── components/
│   │   ├── PromptBox.tsx
│   │   ├── AudioPlayer.tsx
│   │   ├── StoryCard.tsx
│   │   └── RegionGrid.tsx
│   └── styles/
├── backend/
│   ├── routes/
│   │   ├── generate.py        # Story generation endpoint
│   │   ├── image.py           # Image generation endpoint
│   │   └── audio.py           # Audio narration endpoint
│   └── prompts/
│       └── folklore.py        # Claude prompt templates
├── autentico.html             # ← Current prototype (this file)
└── README.md
```

---

## AI Prompt Architecture

The core prompt sent to Claude follows this structure:

```
System:
  You are a master oral storyteller and cultural folklorist.
  Generate authentic folklore from [COUNTRY] in the tradition of
  [FOLKLORE_TYPE]. Draw from real mythological archetypes and
  narrative structures from that culture. Tone: [TONE].

User:
  Generate a [LENGTH] [FOLKLORE_TYPE] from [COUNTRY].
  Art style context: [ART_STYLE].
  Additional detail: [USER_PROMPT]

  Return JSON:
  {
    "title": "...",
    "tagline": "...",
    "story": "...",
    "image_prompt": "...",
    "audio_prompt": "...",
    "cultural_context": "...",
    "tags": [...]
  }
```

---

## Integrations

### Telegram Bot (Planned)
The same generation API can be exposed to a Telegram bot, allowing users to generate stories directly from a chat interface.

```
User: /story Indonesia Origin Myth
Bot:  🌊 Generating your folklore...
      [Returns: title + excerpt + link to full story]
```

See `/backend/telegram/` for bot setup (coming soon).

---

## Mobile Audit Log

| Issue | Status |
|---|---|
| `cursor:none` breaking tap on mobile | ✅ Fixed — cursor only on desktop |
| 6 dropdowns visible at once | ✅ Fixed — collapsed to 2 + Advanced toggle |
| Nav links hidden with no hamburger | ✅ Fixed — full-screen drawer added |
| Hero title too large on 360px screens | ✅ Fixed — `clamp(40px, 8.5vw, 108px)` |
| Prompt box grid overflow on mobile | ✅ Fixed — single column on `< 600px` |
| Generate button too small to tap | ✅ Fixed — full width on mobile |
| Region grid 7-column unusable | ✅ Fixed — 4 col → 3 col responsive |
| Footer breaking at narrow widths | ✅ Fixed — flex-wrap + centered |

---

## Roadmap

- [ ] Connect Claude API for real story generation
- [ ] Integrate image generation (FLUX / SDXL)
- [ ] Integrate voice narration (ElevenLabs)
- [ ] User accounts + story library
- [ ] Telegram bot integration
- [ ] Share to social (link preview with story art)
- [ ] Community feed (public stories)
- [ ] Web3 / NFT minting (optional, Phase 2)

---

## Getting Started

No build step required for the prototype:

```bash
# Just open the file
open autentico.html

# Or serve locally
npx serve .
# → http://localhost:3000/autentico.html
```

---

## License

© 2025 Autentico. All rights reserved.
Stories generated by AI are for creative and educational purposes.
Cultural traditions referenced are the heritage of their respective communities.
