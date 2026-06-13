# Charlamos — App Context for Landing Page

> One-liner: **Practise Spanish on video with a real partner — like Omegle, but with an AI teacher that catches your mistakes live as you chat.**

This document is reference context for building the landing page. It describes what the app is, who it's for, how it works, and the language/positioning already used in the product.

---

## What it is

Charlamos is a browser-based app that pairs you with another Spanish learner over **live video + text chat**. As you type in Spanish, an **AI teacher** checks every message and highlights your mistakes in colour in real time — grammar, spelling/accents, and punctuation — with the correction one hover/tap away. Built-in icebreakers and games keep the conversation flowing.

No app install, no signup, no account. You open the page, pick a name and your level, allow camera + mic, and you're matched.

> ⚠️ **Naming note:** the current name is **Charlamos** (repo name, TURN domain `charlamos.metered.live`, and latest git history). The live UI still renders the old name **"PolyPal"** in a few places (page title, onboarding logo, header). Pick one name for the landing page — and the in-app branding should be updated to match.

---

## Who it's for

- **Intermediate-ish Spanish learners** (the default level is B1) who can already form sentences but want real conversation practice.
- People who learn best by **speaking with a partner**, not drilling flashcards alone.
- Self-directed learners who want **instant correction** without a paid tutor or scheduled class.
- Levels supported, CEFR: **A1 → C1** (Beginner to Advanced).

---

## How it works (user flow)

1. **Onboard** — enter your name and select your Spanish level (A1–C1).
2. **Match** — two ways in:
   - **"Talk to a random stranger"** — drops you into a matchmaking lobby that pairs you with another learner.
   - **"Join a private room"** — enter (or generate) a room code and share it with a friend; you both join the same code.
3. **Talk** — live video call with your partner, plus a text chat where you type in Spanish.
4. **Learn** — every message you send is analysed and corrected inline; a side panel tracks your stats and a running summary of corrections.
5. **Next** — in random mode, hit **⏭ Next** any time to skip to a new partner.

---

## Core features (for feature sections / bullets)

### 🎥 Live video chat with a partner
1-to-1 WebRTC video + audio. Mute/unmute mic, toggle camera, and "Next" to a new stranger. Works across networks (STUN/TURN).

### 👩‍🏫 Live AI Spanish teacher
Checks each message as you send it and highlights issues in three colours:
- 🔴 **Grammar** — conjugation, gender agreement (e.g. *el/la*, *yo soy* vs *yo es*)
- 🟡 **Spelling / accents** — e.g. *esta* → *está*, question-word accents (*como* → *cómo*)
- 🔵 **Punctuation** — opening *¿* and *¡*, capital letters

Hover or tap any highlight to see the fix and a short explanation. Clean messages get a "✓ Perfect!"

### 🎮 Icebreakers & games (shared live in the room)
- 💬 **Icebreaker** — a question to get the chat going
- 📖 **Word of the day** — a fun word + meaning, use it in a sentence (e.g. *sobremesa*, *madrugar*)
- 🖼️ **Describe the scene** — describe an emoji scene in Spanish
- 🎭 **Role-play** — a situation to act out together (restaurant, airport, market…)
- ⚡ **20 Questions** — guess what your partner is thinking with yes/no questions

### 📊 Session stats & summary
Tracks messages sent, mistakes caught, an accuracy %, and a scrollable list of every correction from the session.

### 🤝 Smart, level-aware matchmaking
Prefers pairing you with someone at your **own CEFR level**, but never leaves you waiting — the acceptable level gap widens the longer you wait (same level for the first few seconds, then ±1 band, then anyone), so you always get matched.

---

## Positioning & tone

- **Tagline in product:** "Hop on video with a partner and practise your Spanish — like Omegle, but with an AI teacher that catches your mistakes live and highlights them in colour as you chat."
- **The Omegle comparison** is the strongest hook: *random video chat, but it makes you better at Spanish.*
- Tone is **playful and bilingual** — Spanish accents throughout the UI ("Enviar", "SALA", "TÚ", "o entra en una sala privada"). The signature *¿* mark is used as a visual motif (it's literally the punctuation the app teaches).
- Visual identity (current app): a dark "midnight violet studio" theme — deep violet/purple (`#9d5cff`) with magenta-pink accents (`#e879f9`), serif display font (Fraunces) + clean sans body (Hanken Grotesk), subtle film grain.

---

## Key selling points (landing-page-ready)

| Hook | Why it matters |
|------|----------------|
| **Real conversation, instantly** | Matched with a live partner in seconds — no scheduling, no tutor fees. |
| **Mistakes caught as you go** | Inline colour-coded corrections turn every message into a mini lesson. |
| **No download, no signup** | Runs in the browser. Pick a name, allow camera, go. |
| **Practise with friends or strangers** | Private room codes for a study buddy, random match for everyone else. |
| **Matched at your level** | Level-aware pairing keeps conversations at the right difficulty. |
| **Learning baked into play** | Games and icebreakers mean you never run out of things to say. |

---

## Suggested CTAs

- Primary: **"Talk to a stranger in Spanish"** / **"Empieza a charlar"**
- Secondary: **"Practise with a friend"** (private room)

---

## Technical notes (not for the page, but useful context)

- **Stack:** single static `index.html` (vanilla JS, no framework) + one Vercel serverless function (`api/turn.js`).
- **Realtime signalling:** MQTT over WebSocket (public EMQX broker) for presence, matchmaking lobby, chat, and WebRTC signalling.
- **Video:** WebRTC peer-to-peer with perfect-negotiation; STUN + Metered TURN (credentials fetched server-side so the secret key stays out of the page source).
- **AI teacher (current state):** a **rule-based demo** — a curated set of grammar/gender/accent/punctuation rules, not yet a real LLM. (Worth knowing so the landing page doesn't over-promise; the inline-correction UX is real, the "AI" is currently heuristic.)
- **Privacy angle:** no accounts, no stored chat history; sessions are ephemeral.
