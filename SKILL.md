---
name: local-whisper
description: "Free local speech-to-text using MLX Whisper on Apple Silicon. Free, private, no API costs."
metadata:
  openclaw:
    emoji: "🎤"
    version: "1.1.0"
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

**Free replacement for OpenAI Whisper API.** Runs 100% locally on Apple Silicon.

## What It Replaces

| Service | Cost | Privacy | This Skill |
|---------|------|---------|------------|
| OpenAI Whisper API | $0.006/min | Cloud | **Free, Local** |
| Groq Whisper API | ~$0.001/min | Cloud | **Free, Local** |
| AssemblyAI | $0.01/min | Cloud | **Free, Local** |

**Same quality, zero cost, complete privacy.**

## Performance

- **~1 second** for typical voice messages (Apple Silicon)
- Supports 99 languages
- Translation to English included

## Quick Start

```bash
# 1. Install dependencies
pip3 install -r requirements.txt

# 2. Start daemon (pre-loads model for instant transcription)
python3 scripts/daemon.py

# 3. Transcribe
./scripts/transcribe.sh audio.mp3
```

## How It Works

Uses [MLX Whisper](https://github.com/ml-explore/mlx-examples/tree/main/whisper) — Apple's ML framework optimized for Apple Silicon. The model runs on Neural Engine + GPU for maximum speed.

### Daemon Mode (Recommended)

The daemon keeps the model loaded in memory:

```bash
# Start once
python3 scripts/daemon.py

# Then transcribe instantly
./scripts/transcribe.sh recording.mp3
```

### Direct Mode (No Daemon)

```bash
# Loads model each time (~5s overhead)
python3 scripts/transcriber_cli.py audio.mp3
```

## Auto-Start on Login

```bash
cp com.local-whisper.plist ~/Library/LaunchAgents/
launchctl load ~/Library/LaunchAgents/com.local-whisper.plist
```

## API Endpoint

When daemon is running:

```bash
curl -X POST http://localhost:8787/transcribe \
  -F "file=@audio.mp3"
```

Response:
```json
{"text": "Hello world", "language": "en"}
```

## Translation

Translate any language to English:

```bash
./scripts/transcribe.sh audio_spanish.mp3 --translate
```

## Models

| Model | Speed | Accuracy | RAM |
|-------|-------|----------|-----|
| `medium` (default) | ~1s | Good | 1.5GB |
| `distil-large-v3` | ~2s | Better | 1.5GB |
| `large-v3` | ~3s | Best | 3GB |

Models download automatically on first use.

## Requirements

- macOS with Apple Silicon (M1/M2/M3/M4)
- Python 3.9+
- ~2GB RAM

## License

MIT
