# Netaji_Freedom_Fighter_Video_Generator
# Netaji Subhas Chandra Bose – AI Tribute Video Generator

A Python-based pipeline that automatically generates a short tribute video about an Indian freedom fighter using AI-powered text-to-speech and programmatic visual generation. This project was built as a submission for the **Junior AI Developer** assignment at Sabr Intelligence.

## Overview

This project takes a brief script about Netaji Subhas Chandra Bose and converts it into a fully rendered 10-second video. The pipeline combines:

- AI-generated narration (text-to-speech)
- Programmatically rendered visual slides (text, gradients, fonts)
- Audio-video synchronization and merging

The result is a short, polished tribute video suitable for social media or educational use.

## Features

- Converts text script into natural-sounding speech using Google Text-to-Speech (gTTS)
- Generates clean, styled visual slides with custom fonts and gradient backgrounds
- Synchronizes slide timing with audio duration automatically
- Merges audio and video tracks into a single final `.mp4` file
- Modular code structure — easy to swap in a different freedom fighter, script, or visual theme

## Tech Stack

| Component | Library/Tool |
|---|---|
| Text-to-Speech | gTTS (Google Text-to-Speech) |
| Audio processing | pydub |
| Video/image rendering | matplotlib, Pillow (PIL) |
| Video assembly | moviepy |
| Audio/video encoding | FFmpeg |
| Environment | Python 3.13, Jupyter Notebook |

## Prerequisites

Before running this project, ensure the following are installed:

1. **Python 3.13** (or compatible version)
2. **FFmpeg** — required for audio/video encoding and merging
   - Install via: `winget install -e --id Gyan.FFmpeg` (Windows)
   - Verify installation: `ffmpeg -version`
3. **Required Python packages**:
   ```bash
   pip install gtts pydub moviepy matplotlib pillow
   ```

> **Note:** After installing FFmpeg, restart your terminal and Jupyter Notebook completely (not just the kernel) so the updated system PATH is recognized.

## Project Structure

```
netaji-tribute-video/
│
├── Netaji_Freedom_Fighter_Video_Generator.ipynb   # Main notebook (code)
├── netaji_voice.mp3                                # Generated narration audio
├── netaji_voice_10sec.mp3                          # Trimmed/final audio (10s)
├── slides/                                         # Generated slide images (if saved)
├── Netaji_Subhas_Chandra_Bose_Tribute.mp4          # Final rendered video
└── README.md                                       # This file
```

## How It Works

### 1. Script Definition
A short narration script is defined, broken into key facts about Netaji:
- Introduction and dates (23 Jan 1897 – 18 Aug 1945)
- Famous quote: *"Give me blood, I will give you freedom!"*
- Role as founder of the Azad Hind Fauj (INA)
- Legacy as a symbol of courage and sacrifice

### 2. Audio Generation
The script text is passed to gTTS, which generates an `.mp3` narration file:
```python
from gtts import gTTS
tts = gTTS(text=text, lang='en')
tts.save("netaji_voice.mp3")
```

### 3. Slide/Visual Generation
Four timed slides are defined as `(start_time, end_time, title, subtitle, [details])` tuples, each corresponding to a phase of the narration. Slides are rendered frame-by-frame using matplotlib/PIL with custom fonts and a gradient background.

### 4. Audio-Video Sync
The total slide duration is matched to the trimmed audio duration (10 seconds) to ensure narration and visuals stay in sync throughout playback.

### 5. Final Merge
moviepy (backed by FFmpeg) combines the rendered video frames with the narration audio track into the final `.mp4` output.

## Usage

1. Open `Netaji_Freedom_Fighter_Video_Generator.ipynb` in Jupyter Notebook.
2. Run all cells in order (Cell → Run All).
3. The notebook will:
   - Generate the narration audio
   - Render the visual slides
   - Merge audio and video
4. The final video will be saved as `Netaji_Subhas_Chandra_Bose_Tribute.mp4` in the project directory.

## Known Issues & Fixes

| Issue | Cause | Fix |
|---|---|---|
| `FileNotFoundError: [WinError 2]` | FFmpeg not installed or not in system PATH | Install FFmpeg via `winget install -e --id Gyan.FFmpeg`, then restart terminal/Jupyter |
| Audio sounds too fast/unclear after speeding up | `pydub.effects.speedup()` distorts pitch at high speed ratios | Shorten the script text instead of speeding up audio, so natural-speed narration fits the target duration |
| Audio-video duration mismatch | Slide timings don't match final audio length | Trim/adjust script length until natural narration duration matches total slide duration (10s) |

## Sample Output

The final video is a 10-second tribute consisting of four slides:
1. **NETAJI** — Subhas Chandra Bose, dates and intro
2. **Fearless Leader** — famous quote and orator legacy
3. **Azad Hind Fauj** — INA founding and "Jai Hind" banner
4. **Eternal Inspiration** — closing message, symbol of sacrifice and courage

## Future Improvements

- Add support for multiple freedom fighters via a config file
- Add background music mixed under narration
- Support dynamic duration (not fixed to exactly 10s)
- Add subtitle overlay synced with narration

## Author

Submitted as part of the Junior AI Developer assignment for Sabr Intelligence.

## Sample Output

[Watch the tribute video](https://youtu.be/1_fcXK6oA3E)

