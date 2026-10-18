# 🐸 Ribbit

> An intelligent, modular full-stack platform for building, configuring, and interacting with conversational AI agents equipped with document-grounded RAG, dynamic memory, and end-to-end voice capabilities.

---

## 📌 Overview

**Ribbit** provides a developer-friendly architecture to build, test, and deploy specialized AI agents. Whether you need a customer support bot, a research assistant grounded in uploaded PDFs, or an interactive voice persona, Ribbit provides a decoupled Python backend and React frontend ready for rapid development.

---

## ✨ Key Features

- 🤖 **Custom Agent Management**: Create, customize, and configure agent personas, system prompts, and parameters via an intuitive UI.
- 📚 **Retrieval-Augmented Generation (RAG)**: Ingest documents from local uploads, generate vector embeddings, and retrieve domain knowledge with high semantic precision.
- 🗣️ **Voice & Audio Pipeline**: Built-in modules for Speech-to-Text (STT) and Text-to-Speech (TTS) for natural, fluid spoken conversations.
- 🧠 **Context & Memory Management**: Persist conversational state and chat histories across interactions.
- 🎨 **Responsive Frontend**: Clean React interface featuring agent cards, configuration modals, and an interactive chat widget.
- 🔌 **Modular Architecture**: Decoupled routes, services, and utilities designed for easy integration with OpenAI, Anthropic, Gemini, local LLMs (Ollama/vLLM), and vector databases.

---

## 📂 Project Structure

```text
Ribbit/
├── Data/                             # Local data persistence & assets
│   ├── embeddings/                   # Saved vector indices & embeddings
│   ├── uploads/                      # Uploaded knowledge base documents
│   └── agents.json                   # Agent metadata & configuration profiles
│
├── backend/                          # Backend API service (Python)
│   ├── requirements.txt              # Python package dependencies
│   └── app/
│       ├── __init__.py
│       ├── main.py                   # FastAPI / application entry point
│       ├── routes/
│       │   ├── __init__.py
│       │   ├── agent.py              # Agent CRUD & configuration endpoints
│       │   └── chat.py               # Chat completion & voice dialogue endpoints
│       ├── services/
│       │   ├── llm.py                # LLM client orchestration
│       │   ├── memory.py             # Conversation history & buffer memory
│       │   ├── rag.py                # Document loading, chunking & vector search
│       │   ├── stt.py                # Speech-to-Text audio transcription
│       │   └── tts.py                # Text-to-Speech audio synthesis
│       └── utils/
│           ├── audio.py              # Audio format conversion & helpers
│           ├── config.py             # App settings & environment loader
│           └── file_folder.py        # File upload & path management utilities
│
└── frontend/                         # Frontend client (React + Vite)
    ├── package.json                  # Node.js dependencies & scripts
    └── src/
        ├── App.jsx                   # Root application component & routing
        ├── components/
        │   ├── AgentCard.jsx         # Card component displaying agent profiles
        │   ├── AgentForm.jsx         # Form component to create/edit agents
        │   └── ChatWidget.jsx        # Conversational UI with text & audio input
        ├── pages/
        │   └── Home.jsx              # Main dashboard / landing page
        └── services/
            └── api.jsx               # Backend API communication layer
```

---

## 🛠️ Tech Stack

| Domain | Technology / Libraries |
| :--- | :--- |
| **Backend** | Python 3.10+, FastAPI / Uvicorn, Pydantic |
| **AI / RAG** | LangChain / LlamaIndex / LiteLLM, ChromaDB / FAISS |
| **Audio & Voice** | Whisper / Faster-Whisper (STT), Edge-TTS / Coqui / ElevenLabs (TTS), PyDub |
| **Frontend** | React 18+, Vite, Modern CSS |
| **Data Storage** | Local JSON (`agents.json`), Local Vector Store (`embeddings/`), File System (`uploads/`) |

---

## 🚀 Getting Started

### Prerequisites

- **Python**: 3.10 or higher
- **Node.js**: v18 or higher (with `npm` or `pnpm`)
- **FFmpeg**: Required on your system for audio conversions (`stt.py` / `tts.py`)

---

### 1. Backend Setup

1. **Navigate to the backend directory**:
   ```bash
   cd backend
   ```

2. **Create and activate a virtual environment**:
   - **Windows (PowerShell)**:
     ```powershell
     python -m venv venv
     .\venv\Scripts\Activate.ps1
     ```
   - **Linux / macOS**:
     ```bash
     python3 -m venv venv
     source venv/bin/activate
     ```

3. **Install dependencies**:
   ```bash
   pip install -r requirements.txt
   ```

4. **Configure environment variables**:
   Create a `.env` file in `backend/` with the required keys:
   ```env
   # Application
   HOST=127.0.0.1
   PORT=8000
   DEBUG=True

   # Model Providers
   OPENAI_API_KEY=your_openai_api_key_here
   # GEMINI_API_KEY=your_gemini_api_key_here
   # ANTHROPIC_API_KEY=your_anthropic_api_key_here

   # Data Paths (relative or absolute)
   DATA_DIR=../Data
   UPLOAD_DIR=../Data/uploads
   EMBEDDING_DIR=../Data/embeddings
   ```

5. **Start the backend server**:
   ```bash
   uvicorn app.main:app --reload --host 127.0.0.1 --port 8000
   ```
   *The API will be available at `http://localhost:8000` with interactive docs at `http://localhost:8000/docs`.*

---

### 2. Frontend Setup

1. **Navigate to the frontend directory**:
   ```bash
   cd ../frontend
   ```

2. **Install Node packages**:
   ```bash
   npm install
   ```

3. **Start the development server**:
   ```bash
   npm run dev
   ```
   *The frontend application will run at `http://localhost:5173`.*

---

## 📡 API Overview

The backend exposes RESTful endpoints for agent administration and chat interaction:

### Agent Routes (`/api/agents`)
| Method | Endpoint | Description |
| :--- | :--- | :--- |
| `GET` | `/api/agents` | Retrieve all configured agents |
| `POST` | `/api/agents` | Create a new agent profile |
| `GET` | `/api/agents/{agent_id}` | Fetch details of a specific agent |
| `PUT` | `/api/agents/{agent_id}` | Update agent settings or prompt |
| `DELETE` | `/api/agents/{agent_id}` | Delete an agent profile |

### Chat & Voice Routes (`/api/chat`)
| Method | Endpoint | Description |
| :--- | :--- | :--- |
| `POST` | `/api/chat` | Send a text prompt and receive agent completion |
| `POST` | `/api/chat/voice` | Upload audio input, transcribe (STT), query agent, and return audio response (TTS) |
| `POST` | `/api/chat/upload` | Upload knowledge documents to an agent's RAG index |

---

## 🧭 Roadmap

- [ ] Real-time audio streaming over WebSockets.
- [ ] Tool / function calling support (web search, calculator, custom APIs).
- [ ] Multi-agent orchestration and collaborative workflows.
- [ ] Role-based access control and user authentication.
- [ ] Support for local LLM inference engines (Ollama, LM Studio).

---

## 📄 License

This project is open-source and available under the [MIT License](LICENSE).
