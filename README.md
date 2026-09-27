# 🎥 AI Video Transcription & Meeting Assistant

An AI-powered meeting and video assistant that transforms **YouTube videos or uploaded audio/video files** into structured, searchable information.

The application automatically extracts audio, generates a transcript, and uses an LLM pipeline to produce a **title, summary, action items, key decisions, and open questions**. It also includes a **RAG-based question-answering system** that allows users to ask questions about the processed content.

## ✨ Features

* 🎬 **YouTube & Local File Support**

  * Process YouTube videos using a URL
  * Process uploaded audio/video files

* 🎙️ **AI Speech-to-Text**

  * Local transcription using Whisper
  * Dedicated processing path for Hindi/Hinglish audio

* 📝 **AI-Generated Content**

  * Automatic title generation
  * Structured summaries
  * Action item extraction
  * Key decision extraction
  * Open question extraction

* 🔍 **RAG-Powered Q&A**

  * Convert transcript content into searchable vector representations
  * Retrieve relevant sections from the transcript
  * Ask questions grounded in the processed video/audio

* 🧩 **Modular Pipeline**

  * Audio processing
  * Transcription
  * Content extraction
  * Summarization
  * Vector storage
  * Retrieval and question answering

---

## 🏗️ Architecture

```text
                 ┌─────────────────────┐
                 │   YouTube URL /     │
                 │   Audio / Video     │
                 └──────────┬──────────┘
                            │
                            ▼
                 ┌─────────────────────┐
                 │   Audio Processing  │
                 │  Extract / Prepare  │
                 │       Audio         │
                 └──────────┬──────────┘
                            │
                            ▼
                 ┌─────────────────────┐
                 │    Transcription    │
                 │   Whisper / STT     │
                 └──────────┬──────────┘
                            │
                            ▼
                 ┌─────────────────────┐
                 │     Transcript      │
                 └──────────┬──────────┘
                            │
              ┌─────────────┼─────────────┐
              │             │             │
              ▼             ▼             ▼
       ┌────────────┐ ┌────────────┐ ┌────────────┐
       │  Summary   │ │   Action   │ │  Decisions │
       │  & Title   │ │   Items    │ │ & Questions│
       └────────────┘ └────────────┘ └────────────┘
                            │
                            ▼
                 ┌─────────────────────┐
                 │   Vector Store      │
                 │  Transcript Chunks  │
                 └──────────┬──────────┘
                            │
                            ▼
                 ┌─────────────────────┐
                 │    RAG Pipeline     │
                 │ Retrieval + LLM     │
                 └──────────┬──────────┘
                            │
                            ▼
                 ┌─────────────────────┐
                 │  Context-Aware Q&A  │
                 └─────────────────────┘
```

---

## 🔄 How It Works

### 1. Input Processing

The system accepts either:

* A YouTube URL
* An audio file
* A video file

The input is processed and prepared for transcription.

### 2. Audio Processing

The audio processing module extracts and prepares the audio required for speech recognition.

### 3. Transcription

The processed audio is passed through the transcription pipeline to generate the transcript.

The project also includes a dedicated path for **Hindi/Hinglish audio**, making it suitable for multilingual meeting and video content.

### 4. AI Content Extraction

The transcript is passed through an LLM-based processing pipeline to generate:

* Title
* Summary
* Action items
* Key decisions
* Open questions

This converts a raw transcript into a structured meeting brief.

### 5. Vector Storage

The transcript is divided into meaningful chunks and converted into vector representations.

These embeddings are stored in a vector store so that relevant information can be retrieved later.

### 6. RAG-Based Question Answering

When a user asks a question:

```text
User Question
      ↓
Retrieve Relevant Transcript Chunks
      ↓
Provide Retrieved Context to LLM
      ↓
Generate Context-Grounded Answer
```

This allows users to interact with the video content instead of manually searching through a long transcript.

---

## 📁 Project Structure

```text
AI-Video-Transcription/
│
├── audio_processor.py    # Audio extraction and preprocessing
├── extractor.py           # Content extraction utilities
├── transcriber.py         # Speech-to-text transcription
├── summarize.py           # Title and structured content generation
├── rag_engine.py          # Retrieval-Augmented Generation pipeline
├── vector_store.py        # Vector storage and retrieval
├── main.py                # Application entry point
│
└── README.md
```

---

## 🛠️ Tech Stack

| Technology                   | Purpose                                             |
| ---------------------------- | --------------------------------------------------- |
| **Python**                   | Core application                                    |
| **Whisper / Speech-to-Text** | Audio transcription                                 |
| **LLM**                      | Summarization and structured information extraction |
| **Embeddings**               | Semantic representation of transcript content       |
| **Vector Store**             | Similarity search and retrieval                     |
| **RAG**                      | Context-grounded question answering                 |

---

## 🚀 Getting Started

### Prerequisites

Make sure you have:

* Python 3.10+
* FFmpeg
* Git
* Required API credentials for the LLM services used by the project

### 1. Clone the repository

```bash
git clone https://github.com/Fazl-DE/AI-Video-Transcription.git

cd AI-Video-Transcription
```

### 2. Create a virtual environment

```bash
python -m venv .venv
```

Activate it:

**Linux / macOS**

```bash
source .venv/bin/activate
```

**Windows**

```bash
.venv\Scripts\activate
```

### 3. Install dependencies

```bash
pip install -r requirements.txt
```

### 4. Configure environment variables

Create a `.env` file and add the required API credentials.

```env
# Add your required API keys here
```

> Do not commit your `.env` file to GitHub.

### 5. Run the application

```bash
python main.py
```

---

## 💡 Example Use Case

Imagine a 1-hour technical meeting.

Instead of manually watching the entire recording, the system can generate:

```text
Title:
Project Architecture Discussion

Summary:
The team discussed the backend architecture,
database design, deployment strategy, and API structure.

Action Items:
- Finalize API design
- Prepare deployment configuration
- Review database schema

Key Decisions:
- Use a modular backend architecture
- Introduce semantic search for meeting content

Open Questions:
- Which deployment platform should be used?
- What authentication mechanism should be implemented?
```

The user can then ask:

```text
"What database architecture was discussed?"
```

and the RAG pipeline retrieves the relevant transcript context before generating the answer.

---

## 🧠 Key AI Concepts Demonstrated

This project demonstrates practical implementation of:

* Speech-to-Text
* Large Language Models
* Prompt-based information extraction
* Text chunking
* Embeddings
* Vector databases
* Semantic search
* Retrieval-Augmented Generation (RAG)
* Context-aware question answering
* AI pipeline orchestration

---

## 🔮 Future Improvements

* [ ] Streamlit-based interactive UI
* [ ] LangChain integration
* [ ] LangGraph-based workflow orchestration
* [ ] Multi-speaker diarization
* [ ] Better Hindi/Hinglish transcription
* [ ] Timestamp-based transcript navigation
* [ ] Support for additional video platforms
* [ ] Persistent conversation history
* [ ] Export summaries as PDF/DOCX
* [ ] Authentication and user-specific projects

---

## 🎯 Project Goal

The goal of this project is to transform long-form video and meeting content into **structured, searchable, and actionable knowledge** using modern AI techniques.

Instead of simply producing a transcript, the system creates an intelligent interface for understanding and querying the content.

---

## 👨‍💻 Author

**Fazl-DE**

GitHub: [@Fazl-DE](https://github.com/Fazl-DE)

---

## ⭐ If You Find This Project Useful

If this project helped you understand AI-powered transcription, summarization, or RAG pipelines, consider giving the repository a ⭐.
