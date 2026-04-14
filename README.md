# FGAI — Multimodal Abuse Detection

Detects offensive/abusive language in **Hindi, Tamil, Kannada, and Malayalam** (code-mixed with English) via text or speech input.

**Stack:** Flask · XLM-RoBERTa · Sarvam STT/Translate API · Vanilla JS

---

## Project Structure

```
fgai/
├── index.html          # Frontend UI
├── style.css           # Styles
├── server.py           # Flask backend
├── requirements.txt    # Python dependencies
├── .env.example        # Environment variable template
├── .gitignore
└── model/              # Model folders (NOT committed to Git)
    ├── hindi_en/
    ├── tamil_en/
    ├── kannada_en/
    └── malayalam_en/
```

---

## Local Setup

### 1. Clone the repo
```bash
git clone https://github.com/YOUR_USERNAME/fgai.git
cd fgai
```

### 2. Create a virtual environment
```bash
python -m venv venv
source venv/bin/activate        # macOS/Linux
venv\Scripts\activate           # Windows
```

### 3. Install dependencies
```bash
pip install -r requirements.txt
```

### 4. Set up environment variables
```bash
cp .env.example .env
# Edit .env and add your Sarvam API key:
# SARVAM_API_KEY=your_key_here
```

### 5. Add model weights
Download or copy your fine-tuned models into the `model/` directory:
```
model/hindi_en/
model/tamil_en/
model/kannada_en/
model/malayalam_en/
```
Each folder must contain the standard HuggingFace model files (`config.json`, `tokenizer files`, `model.safetensors` or `pytorch_model.bin`).

> **Note:** Model weights are excluded from Git via `.gitignore`. Use [Git LFS](https://git-lfs.com/), Google Drive, or Hugging Face Hub to share them.

### 6. Run the server
```bash
python server.py
```
Open [http://localhost:5000](http://localhost:5000) in your browser.

---

## Deploying to GitHub

```bash
git init
git add .
git commit -m "Initial commit"
git branch -M main
git remote add origin https://github.com/YOUR_USERNAME/fgai.git
git push -u origin main
```

> ⚠️ **Never commit your `.env` file.** It is already excluded in `.gitignore`. Your Sarvam API key is now read from the environment — set it as a secret/env var on any deployment platform.

---

## API Endpoints

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/health` | Server + model status |
| POST | `/analyze-text` | Analyze typed text |
| POST | `/analyze-speech` | Transcribe audio + analyze |

### `/analyze-text` — Request body
```json
{ "text": "yaar tu bahut bura hai", "language": "hindi" }
```

### `/analyze-speech` — Form data
| Field | Value |
|-------|-------|
| `file` | audio file (WAV/MP3/OGG/WEBM) |
| `language` | `hindi` / `tamil` / `kannada` / `malayalam` |
| `stt_language` | `hi-IN` / `ta-IN` / `kn-IN` / `ml-IN` |

---

## Supported Languages

| Language | Model input | STT code |
|----------|------------|----------|
| Hindi | `hindi` | `hi-IN` |
| Tamil | `tamil` | `ta-IN` |
| Kannada | `kannada` | `kn-IN` |
| Malayalam | `malayalam` | `ml-IN` |
