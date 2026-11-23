# AI Video Assistant with RAG Q&A

Turns a YouTube video or local recording into a transcript, title, summary, action items, decisions and open questions, then answers questions about it with retrieval-augmented generation.

## Credit

The application was written by [Akarsh Vyas](https://github.com/AkarshVyas). The original is [AI-Video-Assistant-](https://github.com/AkarshVyas/AI-Video-Assistant-), which does not include a license. I used it to learn how a transcription and RAG pipeline fits together.

**What I changed:**

- Skip audio chunks too short for Whisper to process
- Convert chunks to 16 kHz mono before transcription
- Move to the `langchain_huggingface` embeddings package

## How it works

1. `yt-dlp` and `pydub` download and split the audio.
2. Whisper (or Sarvam) transcribes it.
3. Mistral writes the summary and extracts key points.
4. Chroma stores the transcript for question answering in Streamlit.

## Run

Requires Python 3.10+ and [FFmpeg](https://ffmpeg.org/).

```bash
pip install -r Requirements.txt
streamlit run app.py
```

Set `MISTRAL_API_KEY` in `.env`. `SARVAM_API_KEY` is needed only for Sarvam transcription. Only process media you have the right to use.
