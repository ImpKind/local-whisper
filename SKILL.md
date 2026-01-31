---
name: local-whisper
description: "Fast local speech-to-text using MLX Whisper on Apple Silicon. Free, private, no API costs."
metadata:
  openclaw:
    emoji: "🎤"
    version: "1.0.0"
    author: "Community"
    repo: "https://github.com/ImpKind/local-whisper"
    requires:
      os: ["darwin"]
      arch: ["arm64"]
      bins: ["python3"]
    install:
      - id: "deps"
        kind: "manual"
        label: "Install dependencies"
        instructions: "pip3 install -r requirements.txt"
---

# Local Whisper

Fast, free, private speech-to-text transcription using MLX Whisper on Apple Silicon.

## Why Local?

- **Free** — No API costs, runs 100% on your Mac
- **Private** — Audio never leaves your machine
- **Fast** — MLX optimized for Apple Silicon (~2-3s for voice messages)
- **Multilingual** — Supports 99 languages + translation to English

## Quick Start

```bash
# Install dependencies
pip3 install -r requirements.txt

# Start the daemon (pre-loads model)
python3 scripts/daemon.py

# Transcribe
./scripts/transcribe.sh audio.mp3
```

## Daemon Mode

The daemon pre-loads the model for instant transcription:

```bash
# Start daemon (default: port 8787, model: medium)
python3 scripts/daemon.py

# Custom options
python3 scripts/daemon.py --port 8787 --model distil-large-v3
```

### Auto-start on Login

```bash
# Copy the LaunchAgent
cp com.local-whisper.plist ~/Library/LaunchAgents/
launchctl load ~/Library/LaunchAgents/com.local-whisper.plist
```

## Scripts

| Script | Purpose |
|--------|---------|
| `transcribe.sh` | Quick transcription (uses daemon if running) |
| `transcribe_large.sh` | Large files with distil-large-v3 model |
| `daemon.py` | HTTP server for fast repeated transcription |

## Models

| Model | Size | Speed | Accuracy |
|-------|------|-------|----------|
| `medium` | 1.4GB | Fast | Good |
| `distil-large-v3` | ~1.5GB | Medium | Better |
| `large-v3` | 2.9GB | Slower | Best |

Models download automatically on first use to `~/.cache/huggingface/`.

## Requirements

- macOS with Apple Silicon (M1/M2/M3)
- Python 3.9+
- ~2GB free RAM for medium model

## Integration

The daemon responds at `http://localhost:8787/transcribe`:

```bash
curl -X POST http://localhost:8787/transcribe \
  -F "file=@audio.mp3" \
  -F "language=en"
```

Response: `{"text": "transcribed text", "language": "en"}`

## License

MIT
