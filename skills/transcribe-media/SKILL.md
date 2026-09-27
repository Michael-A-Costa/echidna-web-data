---
name: transcribe-media
description: Transcribe audio and video files or podcast episodes from a URL into text with timestamps, SRT and WebVTT captions, with optional translation to English. Use when the user wants a transcript, subtitles, or a summary of a recording, meeting, video, or podcast at a URL.
---

# Transcribe audio and video

Use `humble-echidna/audio-transcriber` (Whisper models).

- `mediaUrls`: direct links to audio or video files. For podcasts, use `feeds` with RSS feed URLs and `maxEpisodesPerFeed`.
- `model: "base"` is the default. `"small"` is more accurate and costs more; use it for noisy audio or non-English speech.
- `language`: `"auto"` or an ISO code. `task: "translate"` returns English text for non-English audio.
- Captions: `includeSrt` / `includeVtt` (on by default). `includeWordTimestamps: true` when the user needs word-level timing.
- `maxMinutesPerFile` caps long recordings (default 180).

Long files may still be running when the tool returns; fetch the results with `get-actor-run` and `get-dataset-items`.

Cost on the user's own Apify account: base model $6 per 1,000 audio minutes ($0.36 per hour), small model $15 per 1,000 minutes. Confirm before transcribing more than 3 hours.
