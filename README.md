# MoneyPrinterTurbo — Deutsch online video pipeline

Installation reviewed and verified on 2026-11-04.

## Installed locally

- Upstream: https://github.com/harry0703/MoneyPrinterTurbo
- Version: 1.3.9
- Commit: c8dbf96e9dfee43b30f7c3f440175d6bd4de61de
- Workspace checkout: /workspace/MoneyPrinterTurbo
- Python 3.12.14; isolated .venv; 121 packages installed from uv.lock.
- Local WebUI: http://127.0.0.1:8501 (only accessible within the running environment; not a public deployment).

## Reproduce

```bash
git clone https://github.com/harry0703/MoneyPrinterTurbo.git
cd MoneyPrinterTurbo
git checkout c8dbf96e9dfee43b30f7c3f440175d6bd4de61de
uv sync --frozen --no-dev --python 3.12
cp config.example.toml config.toml
# Set listen_host to 127.0.0.1 and video_source to local in config.toml.
.venv/bin/mpt webui --host 127.0.0.1 --port 8501 --headless
```

Use an already installed Python interpreter if uv cannot download one. FFmpeg is installed in the current environment. Do not commit config.toml, credentials, generated media, storage or .venv.

## Verified

- mpt --version and CLI help succeed.
- Streamlit AppTest loads webui/Main.py with zero exceptions.
- HTTP /_stcore/health returns ok.
- MoviePy/FFmpeg encodes and reads a one-second 320x568 H.264 sample (storage/install-check.mp4).
- Python compilation of app and webui succeeds.

This is an installation/render smoke check, not an end-to-end AI-generated lesson or proof of German/Persian narration quality. No model weights were downloaded for transcription; no paid provider requests, account connections, publication or scheduled production were enabled. Configuration uses local media, loopback binding, empty provider keys and the upstream disabled publishing default. Topic-to-video still needs a configured text backend, permitted media and a working voice backend.

## Assessment

Useful for narrated short-video assembly, subtitles and local/stock material workflows. It is not by itself the established Marta/Lukas audio-driven 3D dialogue pipeline. Existing content, voice, factual-source and cost rules still apply.

The supplied URL is the upstream forks listing, not a chosen fork. The listing was inaccessible through web browsing and the connector rejects the forks REST endpoint. The named alternative https://github.com/Asad-Ismail/MoneyPrinterTurbo-Extended was reviewed at README level: it advertises word highlighting, semantic material matching and local Chatterbox/WhisperX. Those claims were not runtime-tested. Upstream was selected for this installation; the fork was not installed.

Upstream code uses MIT. Media, fonts, music, models and external services require their own license/terms checks before redistribution or production use. A software installation does not establish permission to redistribute bundled assets or guarantee free external inference.

## Scope

This repository records reproducible installation instructions; it does not contain the upstream code or a running hosted service. The installed copy lives in the execution workspace. Previous references in gapmedia-video-automation were not deleted or migrated by this change.
