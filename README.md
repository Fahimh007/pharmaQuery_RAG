# 💊 PharmaQuery — Pharmaceutical Insight Retrieval System

A RAG-powered (Retrieval-Augmented Generation) question-answering application built with **LangChain**, **Google Gemini**, and **Streamlit**. PharmaQuery lets you upload pharmaceutical research documents and ask natural-language questions about them.

---
Live demo: https://pharmaqueryrag-ff9pusxmo6n8zrrlmfwj2j.streamlit.app/

## ✨ Features

- 🔍 **Semantic Search** — Retrieves the most relevant passages from your uploaded documents using vector similarity search.
- 🤖 **AI-Powered Answers** — Generates accurate, context-grounded responses via Google Gemini (`gemini-2.5-flash`).
- 📄 **PDF Ingestion** — Upload one or more pharmaceutical research PDFs to expand the knowledge base.
- 🗃️ **Persistent Vector Store** — Documents are stored in a local ChromaDB database and persist across sessions.
- 🔑 **Flexible API Key Management** — Provide your Gemini API key through the UI or via environment variables.

---
---

## 🚀 Getting Started

### 1. Clone the Repository

```bash
git clone https://github.com/your-username/pharmaquery.git
cd pharmaquery
```

### 2. Install Dependencies

```bash
pip install -r requirements.txt
```

### 3. Set Up Environment Variables

Create a `.env` file in the project root:

```env
GEMINI_API_KEY=your_google_gemini_api_key_here
```

> Alternatively, you can enter your API key directly in the app's sidebar.

### 4. Run the App

```bash
streamlit run app.py
```

The app will open in your browser at `http://localhost:8501`.

---
---

## 🛠️ Tech Stack

| Component | Library / Service |
|---|---|
| UI | [Streamlit](https://streamlit.io/) |
| LLM | [Google Gemini](https://ai.google.dev/) via `langchain-google-genai` |
| Embeddings | `models/gemini-embedding-001` |
| Vector Store | [ChromaDB](https://www.trychroma.com/) |
| PDF Loader | `langchain-community` PyPDFLoader |
| Text Splitter | `SentenceTransformersTokenTextSplitter` (`all-mpnet-base-v2`) |
| RAG Framework | [LangChain](https://www.langchain.com/) |

---

## 📖 How It Works

```
Upload PDF(s)
     │
     ▼
PyPDFLoader extracts text & metadata
     │
     ▼
SentenceTransformers splits text into chunks (size=100, overlap=50)
     │
     ▼
Gemini Embeddings encode chunks → stored in ChromaDB
     │
     ▼
User submits a query
     │
     ▼
Similarity search retrieves top-5 relevant chunks
     │
     ▼
Gemini LLM generates a grounded answer via RAG chain
```

---

## ⚙️ Configuration

| Parameter | Default | Description |
|---|---|---|
| `chunk_size` | `100` | Token chunk size for text splitting |
| `chunk_overlap` | `50` | Overlap between consecutive chunks |
| `search_type` | `similarity` | Retrieval strategy for ChromaDB |
| `k` (top results) | `5` | Number of chunks retrieved per query |
| `temperature` | `1` | LLM response creativity |
| `model` | `gemini-2.5-flash` | Gemini chat model |

---

## 🔑 API Key

You need a **Google Gemini API key** to use this app. Get one for free at [Google AI Studio](https://aistudio.google.com/app/apikey).

Provide it via:
- **`.env` file** — `GEMINI_API_KEY=your_key`
- **Sidebar input** — Enter directly in the running app

