# 🩺 AI Medico Bot

**Intelligent Medical Report Assistant** powered by Retrieval-Augmented Generation (RAG).

Upload a medical report (PDF), and the AI assistant will summarize it, explain medical terms in plain language, and answer your questions — all grounded in the actual content of the report.

---

## ✨ Features

| Feature | Description |
|---|---|
| 📄 **PDF Upload** | Upload any medical report in PDF format |
| 📋 **Report Summary** | Generate a concise, easy-to-understand summary |
| 🔍 **Medical Term Explainer** | Look up terms like *Hemoglobin*, *Creatinine*, etc. |
| 💬 **Medical Q&A** | Ask free-form questions about your report |
| 🩺 **Questions for Doctor** | Get suggested questions to discuss with your physician |
| 📚 **Retrieved Context Viewer** | Inspect the exact chunks and source pages used by the AI |
| 🤖 **Multi-LLM Support** | Google Gemini (2.5 Flash / Pro) and Ollama (Llama 3.2, Mistral, Gemma 3, Phi 4) |
| 🗄️ **Dual Vector DB** | Choose between FAISS and ChromaDB |
| 🧠 **Multiple Embeddings** | MiniLM, BGE Small/Base, E5 Base, MPNet |

---

## 🛠️ Tech Stack

- **Frontend** — [Streamlit](https://streamlit.io/)
- **LLM Framework** — [LangChain](https://www.langchain.com/)
- **LLM Providers** — [Google Gemini](https://ai.google.dev/) · [Ollama](https://ollama.com/)
- **Embeddings** — [HuggingFace Sentence Transformers](https://huggingface.co/sentence-transformers)
- **Vector Stores** — [FAISS](https://github.com/facebookresearch/faiss) · [ChromaDB](https://www.trychroma.com/)
- **PDF Parsing** — PyPDF via LangChain

---

## 🏗️ Architecture

```
Medical Report (PDF)
        │
        ▼
   PDF Loader ──▶ Document Splitter ──▶ Embedding Model
                                              │
                                              ▼
                                     Vector Database
                                      (FAISS / Chroma)
                                              │
        User Question ──▶ Retriever ──────────┘
                              │
                              ▼
                      LLM (Gemini / Ollama)
                              │
                              ▼
                        AI Response
```

---

## 🚀 Getting Started

### Prerequisites

- Python 3.10+
- (Optional) [Ollama](https://ollama.com/) installed locally for local LLM support

### 1. Clone the Repository

```bash
git clone https://github.com/<your-username>/ai-medico-bot.git
cd ai-medico-bot
```

### 2. Create a Virtual Environment

```bash
python -m venv venv
source venv/bin/activate   # Linux / macOS
venv\Scripts\activate      # Windows
```

### 3. Install Dependencies

```bash
pip install streamlit langchain langchain-google-genai langchain-ollama \
            langchain-huggingface langchain-community \
            faiss-cpu chromadb pypdf python-dotenv sentence-transformers
```

### 4. Set Up Environment Variables

Create a `.env` file in the project root:

```env
GOOGLE_API_KEY=your_google_api_key_here
```

> Get a free API key from [Google AI Studio](https://aistudio.google.com/apikey).

### 5. Run the App

```bash
streamlit run app.py
```

The app will open at **http://localhost:8501**.

---

## 📖 Usage

1. **Upload** a medical report PDF via the sidebar.
2. **Configure** the LLM provider, model, vector database, embedding model, and chunk settings.
3. Click **🚀 Build Database** to process the report.
4. Use any of the features:
   - **Generate Summary** — one-click report summary
   - **Explain Medical Term** — enter a term to get a plain-language explanation
   - **Ask AI** — type any question about your report
5. Expand **📚 Retrieved Context** to see the source chunks used by the model.

---

## ⚙️ Configuration Options

| Setting | Options | Default |
|---|---|---|
| LLM Provider | Google Gemini, Ollama | Google Gemini |
| Gemini Models | Gemini 2.5 Flash, Gemini 2.5 Pro | Gemini 2.5 Flash |
| Ollama Models | Llama 3.2, Mistral, Gemma 3, Phi 4 | Llama 3.2 |
| Vector Database | FAISS, ChromaDB | FAISS |
| Embedding Model | MiniLM, BGE Small, BGE Base, E5 Base, MPNet | MiniLM |
| Chunk Size | 500 – 2000 | 1000 |
| Chunk Overlap | 0 – 500 | 200 |
| Top K Retrieval | 1 – 10 | 3 |

---

## 📁 Project Structure

```
ai-medico-bot/
├── app.py                  # Streamlit application (main entry point)
├── utils/
│   ├── __init__.py         # Package exports
│   ├── loader.py           # PDF loading via LangChain
│   ├── splitter.py         # Document chunking
│   ├── embeddings.py       # HuggingFace embedding model manager
│   ├── vectorstore.py      # FAISS & ChromaDB vector store creation
│   ├── llm.py              # LLM provider manager (Gemini / Ollama)
│   ├── prompts.py          # Prompt templates for RAG tasks
│   └── rag_chain.py        # RAG chain orchestration
├── data/                   # Uploaded PDF reports (gitignored)
├── database/               # Persisted vector databases (gitignored)
├── assets/                 # Static assets
├── test_*.py               # Unit / integration tests
├── .env                    # API keys (gitignored)
├── .gitignore
└── README.md
```

---

## ⚠️ Disclaimer

> **AI Medico Bot is for educational and informational purposes only.**
>
> - It does **not** diagnose diseases.
> - It does **not** prescribe medications.
> - It does **not** replace professional medical advice.
> - Always consult a qualified healthcare professional for diagnosis and treatment.

---

## 👨‍💻 Author

**Himanshu Rajak**

---

## 📄 License

This project is intended for educational use. See the repository for license details.
