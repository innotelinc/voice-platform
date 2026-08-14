<p align="center">
  <img src=".github/assets/icon-dark.webp" alt="Voice Platform" width="120" height="120" />
</p>

<h1 align="center">Voice Platform</h1>

<p align="center">
  <strong>The open-source AI voice studio.</strong><br/>
  Clone any voice. Generate speech. Dictate into any app. Talk to agents in voices you own.<br/>
  The full voice I/O stack, running locally on your machine.
</p>

<p align="center">
  <a href="https://github.com/innotelinc/voice-platform/blob/main/LICENSE">
    <img src="https://img.shields.io/github/license/innotelinc/voice-platform?style=flat" alt="License" />
  </a>
</p>

<p align="center">
  <a href="https://voicebox.sh">voicebox.sh</a> •
  <a href="#download">Download</a> •
  <a href="#features">Features</a> •
  <a href="#api">API</a>
</p>

<br/>

## What is Voice Platform?

Voice Platform is a **local-first AI voice studio** — a free and open-source alternative to **ElevenLabs** and **WisprFlow** in one app. Clone voices from a few seconds of audio, generate speech in 23 languages across 7 TTS engines, dictate into any text field with a global hotkey, and give any MCP-aware AI agent a voice of your choosing.

The two cloud incumbents sit on opposite halves of the voice I/O loop — ElevenLabs on output, WisprFlow on input. Voice Platform does both, bridges them with a bundled local LLM for refinement and per-profile personas, and runs the whole thing on your machine.

- **Complete privacy** — models, voice data, and captures never leave your machine
- **7 TTS engines** — Qwen3-TTS, Qwen CustomVoice, LuxTTS, Chatterbox Multilingual, Chatterbox Turbo, HumeAI TADA, and Kokoro
- **Voice cloning and preset voices** — zero-shot cloning from a reference sample, or 50+ curated preset voices
- **23 languages** — from English to Arabic, Japanese, Hindi, Swahili, and more
- **Post-processing effects** — pitch shift, reverb, delay, chorus, compression, and filters
- **Expressive speech** — paralinguistic tags like `[laugh]`, `[sigh]`, `[gasp]` via Chatterbox Turbo
- **Unlimited length** — auto-chunking with crossfade for scripts, articles, and chapters
- **Stories editor** — multi-track timeline for conversations, podcasts, and narratives
- **Voice input** — global dictation hotkey with push-to-talk and toggle modes, in-app mic, Whisper-based STT
- **Agent voice output** — one tool call (`voicebox.speak`) and any MCP-aware agent speaks in a voice you've cloned
- **Voice personalities** — attach a free-form persona to any voice profile, powered by a bundled local LLM
- **API-first** — REST API plus a built-in MCP server for integrating voice I/O into your own apps and agents
- **Native performance** — built with Tauri (Rust), not Electron
- **Runs everywhere** — macOS (MLX/Metal), Windows (CUDA), Linux, AMD ROCm, Intel Arc, Docker

---

## Download

| Platform              | Download                                               |
| --------------------- | ------------------------------------------------------ |
| macOS (Apple Silicon) | [Download DMG](https://voicebox.sh/download/mac-arm)   |
| macOS (Intel)         | [Download DMG](https://voicebox.sh/download/mac-intel) |
| Windows               | [Download MSI](https://voicebox.sh/download/windows)   |
| Docker                | `docker compose up`                                    |

> **Linux** — See [voicebox.sh/linux-install](https://voicebox.sh/linux-install) for build-from-source instructions.

---

## Features

### Multi-Engine Voice Cloning

Seven TTS engines with different strengths, switchable per-generation:

| Engine                      | Languages | Strengths                                                                                                                                |
| --------------------------- | --------- | ---------------------------------------------------------------------------------------------------------------------------------------- |
| **Qwen3-TTS** (0.6B / 1.7B) | 10        | High-quality multilingual cloning, delivery instructions ("speak slowly", "whisper")                                                     |
| **Qwen CustomVoice**        | 10        | 9 curated preset voices with natural-language delivery control — no reference audio required                                             |
| **LuxTTS**                  | English   | Lightweight (~1GB VRAM), 48kHz output, 150x realtime on CPU                                                                              |
| **Chatterbox Multilingual** | 23        | Broadest language coverage — Arabic, Danish, Finnish, Greek, Hebrew, Hindi, Malay, Norwegian, Polish, Swahili, Swedish, Turkish and more |
| **Chatterbox Turbo**        | English   | Fast 350M model with paralinguistic emotion/sound tags                                                                                   |
| **TADA** (1B / 3B)          | 10        | HumeAI speech-language model — 700s+ coherent audio, text-acoustic dual alignment                                                        |
| **Kokoro**                  | 8         | 50 curated preset voices, tiny 82M model, fast CPU inference                                                                             |

### Post-Processing Effects

8 audio effects powered by Spotify's `pedalboard` library. Apply after generation, preview in real time, build reusable presets.

| Effect           | Description                                   |
| ---------------- | --------------------------------------------- |
| Pitch Shift      | Up or down by up to 12 semitones              |
| Reverb           | Configurable room size, damping, wet/dry mix  |
| Delay            | Echo with adjustable time, feedback, and mix  |
| Chorus / Flanger | Modulated delay for metallic or lush textures |
| Compressor       | Dynamic range compression                     |
| Gain             | Volume adjustment (-40 to +40 dB)             |
| High-Pass Filter | Remove low frequencies                        |
| Low-Pass Filter  | Remove high frequencies                       |

### Global Dictation & Voice Input

Hold a hotkey anywhere on your system, speak, release — on macOS the transcript pastes straight into the focused text field. Or hit the mic on any text input and dictate directly into the app.

- Configurable chord bindings — hold-to-speak and tap-to-toggle
- Target-aware paste (macOS) with clipboard save/restore
- Optional LLM refinement of ums, stutters, and false starts
- On-screen pill surfacing `recording`, `transcribing`, `refining`, and `speaking` states

### Speech-to-Text

OpenAI Whisper runs locally on MLX (Apple Silicon) or PyTorch (CUDA / ROCm / DirectML / CPU). Sizes: Base / Small / Medium / Large, plus Turbo (~8x faster than Large).

### Agent Voice Output

One tool call and any MCP-aware agent (Claude Code, Cursor, Cline) speaks in a voice you've cloned — task completions, questions, notifications.

### Voice Personalities

Attach a free-form personality to any voice profile. A bundled Qwen3 LLM powers Compose (fresh in-character lines) and Speak-in-character (rewrites input through the persona before TTS). Agents reach the same path over MCP with `personality: true`.

### GPU Support

| Platform              | Backend        | Notes                                          |
| --------------------- | -------------- | ---------------------------------------------- |
| macOS (Apple Silicon) | MLX (Metal)    | 4-5x faster via Neural Engine                  |
| Windows (NVIDIA)      | PyTorch (CUDA) | Auto-downloads CUDA binary from within the app |
| Linux (NVIDIA)        | PyTorch (CUDA) | Local/remote Python backend with CUDA PyTorch  |
| Linux (AMD)           | PyTorch (ROCm) | Auto-configures HSA_OVERRIDE_GFX_VERSION       |
| Windows (any GPU)     | DirectML       | Universal Windows GPU support                  |
| Intel Arc             | IPEX/XPU       | Intel discrete GPU acceleration                |
| Any                   | CPU            | Works everywhere, just slower                  |

---

## API

Voice Platform exposes a REST API for integrating voice I/O into your own apps and agents.

```bash
# Generate speech
curl -X POST http://127.0.0.1:17493/generate \
  -H "Content-Type: application/json" \
  -d '{"text": "Hello world", "profile_id": "abc123", "language": "en"}'

# Agent voice output — any app or script can speak in a cloned voice
curl -X POST http://127.0.0.1:17493/speak \
  -H "Content-Type: application/json" \
  -H "X-Voicebox-Client-Id: my-script" \
  -d '{"text": "Deploy complete.", "profile": "Morgan"}'

# Transcribe an audio file
curl -X POST http://127.0.0.1:17493/transcribe \
  -F "audio=@recording.wav" \
  -F "model=whisper-turbo"

# List voice profiles
curl http://127.0.0.1:17493/profiles
```

### MCP server

A built-in **Model Context Protocol** server lets any MCP-aware agent speak, transcribe, and browse captures and profiles.

```bash
claude mcp add voicebox \
  --transport http \
  --url http://127.0.0.1:17493/mcp \
  --header "X-Voicebox-Client-Id: claude-code"
```

Four tools ship: `voicebox.speak`, `voicebox.transcribe`, `voicebox.list_captures`, `voicebox.list_profiles`. Full API documentation is available at `http://127.0.0.1:17493/docs`.

---

## Tech Stack

| Layer         | Technology                                                                      |
| ------------- | ------------------------------------------------------------------------------- |
| Desktop App   | Tauri (Rust)                                                                    |
| Frontend      | React, TypeScript, Tailwind CSS                                                 |
| State         | Zustand, React Query                                                            |
| Backend       | FastAPI (Python)                                                                |
| TTS Engines   | Qwen3-TTS, Qwen CustomVoice, LuxTTS, Chatterbox, Chatterbox Turbo, TADA, Kokoro |
| STT           | Whisper / Whisper Turbo (PyTorch or MLX)                                        |
| Local LLM     | Qwen3 (0.6B / 1.7B / 4B), shared runtime with TTS / STT                         |
| MCP Server    | FastMCP mounted at `/mcp` (Streamable HTTP) + bundled stdio shim binary         |
| Effects       | Pedalboard (Spotify)                                                            |
| Inference     | MLX (Apple Silicon) / PyTorch (CUDA/ROCm/XPU/CPU)                               |
| Database      | SQLite                                                                          |

---

## Development

See [CONTRIBUTING.md](CONTRIBUTING.md) for detailed setup and contribution guidelines.

### Quick Start

```bash
git clone https://github.com/innotelinc/voice-platform.git
cd voice-platform

just setup   # creates Python venv, installs all deps
just dev     # starts backend + desktop app
```

Install [just](https://github.com/casey/just): `brew install just` or `cargo install just`. Run `just --list` to see all commands.

**Prerequisites:** [Bun](https://bun.sh), [Rust](https://rustup.rs), [Python 3.11+](https://python.org), [Tauri Prerequisites](https://v2.tauri.app/start/prerequisites/), and [Xcode](https://developer.apple.com/xcode/) on macOS.

### Project Structure

```
voice-platform/
├── app/              # Shared React frontend
├── tauri/            # Desktop app (Tauri + Rust)
├── web/              # Web deployment
├── backend/          # Python FastAPI server
├── landing/          # Marketing website
└── scripts/          # Build & release scripts
```

---

## Contributing

Contributions welcome! See [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines.

1. Fork the repo
2. Create a feature branch
3. Make your changes
4. Submit a PR

## Security

Found a security vulnerability? Please report it responsibly. See [SECURITY.md](SECURITY.md) for details.

---

## License

MIT License — see [LICENSE](LICENSE) for details.
