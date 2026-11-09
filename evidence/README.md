# Provider render evidence

Generated 2026-11-09 from branch `enhancement/tts-provider-adapters` with live API keys from a gitignored `.env`. Each provider rendered a one-scene title video through `src/render.py` at 24 fps; the frame below was extracted around t=1s and the narration audio is the actual TTS output.

**Contact sheet:** [`contact-sheet.png`](contact-sheet.png)

Specs: [`specs/`](specs/) — the exact JSON used for each render.

| Provider | Model / voice | Narration | Video | Frame | Log |
|---|---|---|---|---|---|
| Mistral Voxtral | `voxtral-mini-tts-2603` / `gb_jane_neutral` | [`audio/mistral.wav`](audio/mistral.wav) (1.04s, WAV) | 2.04s | [`frames/mistral.png`](frames/mistral.png) | [`logs/mistral.txt`](logs/mistral.txt) |
| Google Gemini | `gemini-3.8-flash-tts` / `Kore` | [`audio/google.wav`](audio/google.wav) (1.60s, WAV) | 2.60s | [`frames/google.png`](frames/google.png) | [`logs/google.txt`](logs/google.txt) |
| ElevenLabs | `eleven_multilingual_v2` / Sarah (free-tier default) | [`audio/elevenlabs.mp3`](audio/elevenlabs.mp3) (1.44s, MP3) | 2.44s | [`frames/elevenlabs.png`](frames/elevenlabs.png) | [`logs/elevenlabs.txt`](logs/elevenlabs.txt) |
| fal.ai | `fal-ai/elevenlabs/tts/eleven-v3` / Rachel | [`audio/fal.mp3`](audio/fal.mp3) (1.96s, MP3) | 2.96s | [`frames/fal.png`](frames/fal.png) | [`logs/fal.txt`](logs/fal.txt) |

## How it was produced

```bash
set -a; . ./.env; set +a
python3 src/render.py evidence/specs/<provider>.json \
  --workdir temp/evidence-render/cache-<provider> \
  -o temp/evidence-render/<provider>.mp4
```

Full MP4/PPTX outputs were rendered and decoded locally but are not committed, to keep the PR small. The committed screenshots, MP3/WAV narration, and render logs are the evidence. `logs/tests.txt` is the full 13-test mocked-provider-and-CLI suite output.

Both video and narration files were decoded with MoviePy before extraction. No API keys are present in this directory.
