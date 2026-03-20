<!--
Suggested GitHub Topics: whisper semantic-search pdf llm go gemini openai video-search
-->

# Ctrl-f

An open-source, file-driven AI parser that lets you semantically search and highlight content inside PDFs and videos—instantly and accurately.

> The hosted demo (ctrl-f.world) is currently offline due to API token limits. See local setup instructions below.

---

## Contributors

- **Rumen Mitov** — Backend Lead
  <https://www.linkedin.com/in/rumen-mitov>
- **Bilal Waraich** — Whisper & Video‐STS Lead
  <https://www.linkedin.com/in/bilal-waraich-723878296>
- **Felipe Ribadeneira** — VLLM & Prompt Engineering Lead
  <https://www.linkedin.com/in/felipe-ribadeneira>
- **Nikolay Tsonev** — Performance & Optimization Lead
  <https://www.linkedin.com/in/nikolay-tsonev-a8a498226>

---

## Purpose

**Ctrl-f** bridges the gap between powerful LLMs and real-world documents/videos. Conventional LLMs often:

1. Provide unverifiable outputs with poor citation.
2. Struggle to pinpoint within large, image-rich PDFs or long videos.

Ctrl-f solves this by combining:
- **Semantic search** via Google Gemini 2.0-Flash
- **Precise text-layer location** with PyMuPDF & pdfplumber
- **Video transcript indexing** using OpenAI Whisper

End result: Get "golden nuggets" of information—complete with page numbers or timestamps—without wading through hundreds of pages or minutes of footage.

---

## Architecture

### Frontend
- **Tech stack:** HTML, CSS, JavaScript
- **Communication:** JSON over REST APIs

### Backend
- **Core language:** Go (hosted on Google Cloud for auto-scaling)
- **AI & parsing tools:**
  - Google Gemini 2.0-Flash for semantic understanding
  - PyMuPDF & pdfplumber for PDF text extraction
  - OpenAI Whisper for audio transcription
- **Data flow:**
  1. **User query** → Gemini → returns relevant text or timestamps
  2. **PDF path/words** → PyMuPDF/pdfplumber locate exact coords → highlight
  3. **Video URL** → download & strip audio → Whisper transcribes → timestamps from Gemini → frontend auto-seek

All interactions between components use well-structured JSON "contracts" to ensure consistency and debuggability.

---

## Why Ctrl-f Is Unique

- **Hybrid AI pipeline:** Leverages both LLMs and traditional parsers for accuracy.
- **Open source:** No paywalls—anyone can host or extend the tool.
- **Multimedia support:** Works seamlessly on text (PDF) and audio/video.
- **Citation-ready:** Outputs contextual snippets with precise locations, eliminating guesswork and plagiarism risk.

---

## Local Setup

### Prerequisites

- Python 3.9+
- Go 1.21+
- A Google Gemini API key
- An OpenAI API key (for Whisper)

### Steps

1. **Clone the repository**
   ```bash
   git clone https://github.com/your-org/ctrl-f.git
   cd ctrl-f
   ```

2. **Install Python dependencies**
   ```bash
   pip install -r requirements.txt
   ```

3. **Set environment variables**
   ```bash
   export GEMINI_API_KEY=your_gemini_key
   export OPENAI_API_KEY=your_openai_key
   ```

4. **Start the Go backend**
   ```bash
   cd backend/server
   go run .
   ```

5. **Open the frontend**
   Open `index.html` (or `src/landing-page/landing-page.html`) with a local HTTP server or Live Server extension.

### Running the PDF feature directly

```bash
cd backend
python main.py "path/to/your.pdf" "your search query"
```

### Running the video feature directly

```bash
cd backend/transcriber
python Video-Transriber.py "https://youtube.com/watch?v=..."
```
