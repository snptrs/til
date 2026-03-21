# Extracting the audio from a YouTube video

## Install YT-DLP

[yt-dlp](https://github.com/yt-dlp/yt-dlp)is a really useful tool for downloading audio and video from a variety of sources.

```bash
brew install yt-dlp
```

## Get the audio track

```bash
yt-dlp -x --audio-format wav https://www.youtube.com/watch?v=Yt12345
```

- `x`, `--extract-audio` (requires ffmpeg and ffprobe)
- `--audio-format` ‘best’ is the default. Also accepts aac, alac, flac, m4a, mp3, opus, vorbis, wav

