# AI Video Translation & Automated Dubbing System

An end-to-end, multimodal AI pipeline designed to automate video translation and voice dubbing. The system processes an Arabic spoken video, transcribes the speech with context-aware prompts, leverages advanced LLMs for text correction and translation, synthesizes high-quality English voiceovers, and performs audio engineering (background music mixing + delay syncing) before generating the final dubbed video.

## 🚀 Features
- **Advanced Speech-to-Text (STT):** Utilizes `faster-whisper` (Turbo model) with Voice Activity Detection (VAD) and custom initial prompting to capture specialized vocabulary (e.g., ERP systems, workflow terms) accurately.
- **LLM-Powered Translation & Refinement:** Integrates OpenRouter API (`gpt-mini-latest`) to fix raw ASR transcriptions and translate them into professional, natural-sounding English optimized for voice acting.
- **High-Fidelity TTS Synthesis:** Generates fluid English voiceovers using `edge-tts` (`en-US-JennyNeural`).
- **Professional Audio Mixing:** Leverages `pydub` to overlay background music, control relative volume decibels (-5dB adjustments), and add precise silence delays (3000ms) for seamless voice alignment.
- **Video Multiplexing:** Uses `moviepy` and `FFmpeg` to mux the engineered audio track back into the original video while keeping high-definition video rendering (`libx264`/`aac`).

## 🛠️ Tech Stack & Libraries
- **Core Language:** Python 3.x
- **Speech Recognition:** `faster-whisper` (Turbo Model)
- **Translation API:** OpenRouter (`~openai/gpt-mini-latest`)
- **Speech Synthesis:** `edge-tts`
- **Audio & Video Processing:** `pydub`, `moviepy`, `FFmpeg`
- **Development Environment:** Google Colab

## ⚙️ How the Pipeline Works
1. **Audio Extraction:** Extracts the raw `.wav` audio from the source `.mp4` video via FFmpeg.
2. **Context-Aware Transcription:** Transcribes Arabic audio into text using `faster-whisper` assisted by custom jargon context mapping.
3. **Contextual Translation:** OpenRouter polishes the Arabic ASR output and translates it into spoken English.
4. **Voice Synthesis:** `edge-tts` converts the translation into a high-quality `.mp3` voice file.
5. **Audio Engineering:** `pydub` reduces background music volume, injects a 3-second preparatory delay to the voice track, and merges both tracks into a balanced master audio stream.
6. **Final Rendering:** `moviepy` merges the master audio track back into the original video frame structure to produce `final_output.mp4`.

## 💻 Setup & Usage Instruction

### Prerequisites
The environment requires `ffmpeg` for media extraction. Install the core dependencies using:
```bash
!sudo apt update && sudo apt install ffmpeg
!pip install faster-whisper requests edge-tts pydub moviepy
