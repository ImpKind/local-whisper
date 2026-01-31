# 🎤 Local Whisper

[![ClawdHub](https://img.shields.io/badge/ClawdHub-whisper--mlx--local-orange)](https://clawdhub.com/skills/whisper-mlx-local)

Fast, free, private speech-to-text using MLX Whisper on Apple Silicon.

## Features

- **100% Local** — No cloud, no API keys, no costs
- **Private** — Audio never leaves your machine
- **Fast** — MLX optimized for Apple Silicon (2-3s for voice messages)
- **Multilingual** — 99 languages + translation to English
- **Daemon Mode** — Pre-loaded model for instant transcription

## Installation

```bash
# Via ClawdHub
clawdhub install whisper-mlx-local

# Or manually
git clone https://github.com/ImpKind/whisper-mlx-local
cd whisper-mlx-local
pip3 install -r requirements.txt
```

## Usage

```bash
# Quick transcription
./scripts/transcribe.sh recording.mp3

# With translation to English
./scripts/transcribe.sh recording.mp3 --translate

# Large files (uses larger model)
./scripts/transcribe_large.sh long_recording.mp3
```

## Daemon Mode

For fast repeated transcription, run the daemon:

```bash
python3 scripts/daemon.py
```

The daemon pre-loads the model and serves HTTP at `localhost:8787`.

### Auto-start on Login

```bash
cp com.whisper-mlx-local.plist ~/Library/LaunchAgents/
launchctl load ~/Library/LaunchAgents/com.whisper-mlx-local.plist
```

## Requirements

- **macOS** with Apple Silicon (M1/M2/M3/M4)
- **Python 3.9+**
- **~2GB RAM** for the medium model

## How It Works

Uses [MLX Whisper](https://github.com/ml-explore/mlx-examples/tree/main/whisper) — Apple's machine learning framework optimized for Apple Silicon. Models run on the Neural Engine and GPU for maximum speed.

## License

MIT

---

*Free as in freedom. Free as in beer. 🍺*
