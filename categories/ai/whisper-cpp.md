# Install and use whisper.cpp with Core ML on macOS

## Prerequisites

**Xcode** (full app, not just Command Line Tools) — install from the App Store, then run:

```bash
sudo xcode-select -s /Applications/Xcode.app/Contents/Developer
sudo xcodebuild -license accept
```

**Homebrew packages:**

```bash
brew install cmake ffmpeg
```

## Step 1 — Clone the repo

```bash
git clone https://github.com/ggml-org/whisper.cpp.git
cd whisper.cpp
```

## Step 2 — Download the model

```bash
bash ./models/download-ggml-model.sh medium-q8_0
```

This downloads `models/ggml-large-v3.bin`.

## Step 3 — Generate the Core ML encoder

Run the conversion using `uv`, forcing Python 3.11 and a NumPy 1.x pin to avoid compatibility issues with `coremltools`:

```bash
uv run \
  --python 3.11 \
  --with "numpy<2" \
  --with ane_transformers \
  --with openai-whisper \
  --with coremltools \
  models/convert-whisper-to-coreml.py --model medium --encoder-only True
```

## Step 4 — Compile the Core ML model

```bash
xcrun coremlc compile models/coreml-encoder-medium.mlpackage models/
```

## Step 5 — Rename to what whisper.cpp expects

```bash
mv models/ggml-medium-q8_0-encoder.mlmodelc models/ggml-medium-encoder.mlmodelc
```

## Step 6 — Build whisper.cpp with Core ML support

```bash
cmake -B build -DWHISPER_COREML=1
cmake --build build --config Release -j$(sysctl -n hw.logicalcpu)
```

## Step 7 — Transcribe audio

whisper-cli only accepts **16-bit WAV** files. Convert your audio first with ffmpeg:

```bash
ffmpeg -i your-file.mp4 -ar 16000 -ac 1 -c:a pcm_s16le output.wav
```

Then transcribe:

```bash
./build/bin/whisper-cli -m models/ggml-medium-q8_0.bin -f output.wav
```

On the first run you'll see `whisper_init_state: first run on a device may take a while...` — this is normal. Apple's Neural Engine compiles the Core ML model to a device-specific format and caches it. Subsequent runs will be significantly faster.

## Useful flags

| Flag           | Description                           |
| -------------- | ------------------------------------- |
| `-l fr`        | Set input language (e.g. French)      |
| `--output-vtt` | Save output as a `.vtt` subtitle file |
| `--output-srt` | Save output as a `.srt` subtitle file |
| `-t 8`         | Number of threads to use              |
| `--translate`  | Translate to English                  |
| `-ml 1`        | Word-level timestamps                 |

