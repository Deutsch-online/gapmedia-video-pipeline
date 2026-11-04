# ChatGPT and German video setup — 2026-11-04

The local MoneyPrinterTurbo 1.3.9 install now runs an actual prepared-script video through the upstream pipeline, with Edge German narration and timed subtitles.

## Applied changes
- LLM provider selected: openai_codex (ChatGPT device-code flow). Account sign-in is pending; no text model selected or inference verified yet.
- Local media remains selected. No paid material source or automatic publisher enabled.
- UI defaults: German de-DE, de-DE-KatjaNeural-Female, no background music, BeVietnamPro-Medium.ttf, and no server-side folder opening.
- patches/mpt-proxy-ca.patch adds the configured HTTPS proxy and supplements edge-tts's certifi TLS context with SSL_CERT_FILE / REQUESTS_CA_BUNDLE. Certificate and hostname verification remain enabled.

The patch accesses edge-tts's private _SSL_CTX hook; it is specific to the pinned dependency edge-tts 7.3.1. Recheck this integration before updating dependencies. An invalid configured CA file intentionally fails instead of disabling validation.

## Apply on the pinned checkout
From the MoneyPrinterTurbo checkout at c8dbf96e9dfee43b30f7c3f440175d6bd4de61de:
```bash
git apply --check /path/to/gapmedia-video-pipeline/patches/mpt-proxy-ca.patch
git apply /path/to/gapmedia-video-pipeline/patches/mpt-proxy-ca.patch
```

In config.toml select app.llm_provider = "openai_codex"; keep real credentials outside this repository. In WebUI choose OpenAI - Codex, then Connect ChatGPT with a code. Complete sign-in on OpenAI's page, select a compatible model, and Test LLM Connection. Device-code access must be allowed by the account. The separate Native OAuth provider needs the browser and runtime on the same computer, so it is not selected for this remote environment.

## Observed validation
- A real request to Edge produced German speech and word timing.
- CLI ran with prepared text "Guten Morgen! Wie geht es Ihnen? Mir geht es gut, danke.", an original typography PNG, local media, no music and Edge subtitles.
- The upstream pipeline completed, producing H.264 1080x1920 video (6.466667 seconds) and audio (6.460000 seconds), plus a nonempty subtitle file.
- ffprobe verified video/audio streams; a frame was decoded and visually inspected. Voice audio was not independently listened to or judged by ASR.
- A focused check confirms proxy forwarding, word-boundary selection, certificate validation and hostname verification remain active.
- Preview local path: /workspace/deutsch-online-preview.mp4. Generated media and credentials are excluded from commits.

This is a technical preview, not a complete 60-second published lesson, factual-source review, cloned-character/lip-sync example, or successful topic-to-script ChatGPT acceptance. The local media stage uses the explicitly supplied original image; it does not silently generate or fetch external media.
