# 🎤 Local Whisper

[![ClawdHub](https://img.shields.io/badge/ClawdHub-whisper--mlx--local-orange)](https://clawdhub.com/skills/whisper-mlx-local)
[![GitHub](https://img.shields.io/badge/GitHub-ImpKind%2Flocal--whisper-blue?logo=github)](https://github.com/ImpKind/local-whisper)

**Free replacement for OpenAI Whisper API.** 

Runs 100% locally on your Mac. No API keys, no costs, no data leaving your machine.

## Why Use This?

| | OpenAI API | This Skill |
|---|------------|------------|
| **Cost** | $0.006/min | **Free** |
| **Privacy** | Sent to cloud | **Stays local** |
| **Speed** | Network + processing | **~1 second** |
| **API Key** | Required | **Not needed** |

Same Whisper model, zero cost.

## Requirements

- **macOS** with Apple Silicon (M1/M2/M3/M4)
- **Python 3.9+**

## Installation

```bash
# Clone
git clone https://github.com/ImpKind/local-whisper
cd local-whisper

# Install dependencies
pip3 install -r requirements.txt
```

## Usage

### Start the Daemon (Recommended)

The daemon pre-loads the model for instant transcription:

```bash
python3 scripts/daemon.py
```

Then transcribe:

```bash
./scripts/transcribe.sh recording.mp3
```

### Auto-Start on Login

```bash
cp com.local-whisper.plist ~/Library/LaunchAgents/
launchctl load ~/Library/LaunchAgents/com.local-whisper.plist
```

### Translate to English

```bash
./scripts/transcribe.sh audio_german.mp3 --translate
```

## API

When daemon is running at `localhost:8787`:

```bash
curl -X POST http://localhost:8787/transcribe -F "file=@audio.mp3"
```

```json
{"text": "transcribed text", "language": "en"}
```

## How It Works

Uses [MLX Whisper](https://github.com/ml-explore/mlx-examples/tree/main/whisper) optimized for Apple Silicon. The model runs on Neural Engine + GPU.

## License

MIT

---

*Free as in freedom. Free as in beer.* 🍺
