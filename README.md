# 📄 AI Document Assistant

An AI-powered **Document Intelligence System** built for **Alpha IT Managed Services**. Employees can upload a company PDF (employee handbook, HR policy, SOP manual, etc.) and ask questions in natural language instead of manually searching through hundreds of pages.

The app uses a **Retrieval-Augmented Generation (RAG)** pipeline built with **LangChain**, **FAISS**, and **ChatGroq**, with a clean **Streamlit** interface.

---

## 🎯 Problem Statement

Employees spend a significant amount of time searching through lengthy documents such as HR policies, technical manuals, cybersecurity guidelines, and software documentation. This project provides an assistant that:

- Reads and understands an uploaded PDF
- Finds precise answers using semantic search
- Shows the **source document, retrieved chunks, and page numbers**
- Saves time and improves productivity

---

## ✨ Features

- Upload any company PDF document
- One-click **Process Document** button that builds the knowledge base
- Ask questions in plain English
- Retrieves only the most relevant chunks (semantic search)
- AI-generated answers grounded in the retrieved context
- Displays the final answer, source file, retrieved chunks, and page numbers
- Status indicator showing processing progress

---

## 🧰 Tech Stack

| Technology | Purpose |
|---|---|
| **Python** | Programming language |
| **Jupyter Notebook** | Backend development (RAG pipeline) |
| **Streamlit** | User interface |
| **LangChain** | RAG framework |
| **PyPDFLoader** | Load PDF documents |
| **RecursiveCharacterTextSplitter** | Split text into chunks |
| **HuggingFace Embeddings** | Convert text into vectors |
| **FAISS** | Vector database |
| **Retriever** | Retrieve relevant chunks |
| **PromptTemplate** | Build the LLM prompt |
| **ChatGroq** | Generate the AI response |

---

## 📁 Project Structure

```
AI_Document_Assistant/
│
├── data/
│   └── employee_handbook.pdf      # Sample corporate document (80–100 pages)
│
├── backend/
│   └── rag_pipeline.ipynb         # RAG pipeline development notebook
│
├── frontend/
│   └── app.py                     # Streamlit application
│
├── requirements.txt               # Python dependencies
└── README.md                      # Project documentation
```

---

## 🔄 Workflow

```
User
  │
  ▼
Upload PDF (Streamlit)
  │
  ▼
Click "Process Document"
  │
  ▼
┌─────────── Backend Logic ───────────┐
│  1. Load PDF (PyPDFLoader)          │
│  2. Split into Chunks               │
│  3. Generate Embeddings             │
│  4. Create FAISS Database           │
└─────────────────────────────────────┘
  │
  ▼
Ask Question (Streamlit)
  │
  ▼
Retriever  ──►  Most Relevant Chunks
  │
  ▼
PromptTemplate (question + context)
  │
  ▼
ChatGroq LLM
  │
  ▼
Display Answer + Page Numbers
```

### Step-by-step

1. **Upload PDF**: the user uploads a document through the Streamlit interface.
2. **Process Document**: the app loads the PDF, creates LangChain `Document` objects, splits them into chunks, generates embeddings, and builds a FAISS vector store.
3. **Ask a Question**: the user types a natural-language query.
4. **Retrieve**: the retriever fetches only the top-k most relevant chunks from FAISS.
5. **Generate**: the retrieved context and the question are inserted into a `PromptTemplate` and sent to ChatGroq.
6. **Display**: the final answer, retrieved chunks, source file, and page numbers are shown.

---

## 🖥️ Application Layout

The Streamlit interface contains the following sections:

1. **Upload Company Document**: PDF file uploader
2. **Process Document**: builds the knowledge base
3. **Ask Your Question**: text input
4. **Get Answer**: triggers retrieval and generation
5. **Retrieved Information**: source file, number of relevant chunks, and pages
6. **Answer**: AI-generated response based on the retrieved context
7. **Page Number**: pages the answer was drawn from
8. **Status**: confirmation such as *"Document Processed Successfully"*

---

## ⚙️ Installation & Setup

### 1. Clone the repository

```bash
git clone <your-repository-url>
cd AI_Document_Assistant
```

### 2. Create and activate a virtual environment (recommended)

```bash
python -m venv venv

# Windows
venv\Scripts\activate

# macOS / Linux
source venv/bin/activate
```

### 3. Install dependencies

```bash
pip install -r requirements.txt
```

### 4. Set your Groq API key

Get a free API key from the [Groq Console](https://console.groq.com/).

```bash
# Windows (PowerShell)
$env:GROQ_API_KEY="your_api_key_here"

# macOS / Linux
export GROQ_API_KEY="your_api_key_here"
```

> ⚠️ Never commit your API key to GitHub. Use environment variables or a `.env` file listed in `.gitignore`.

---

## ▶️ Running the Application

### Backend (optional: explore the pipeline)

Open the notebook to see and test the RAG pipeline step by step:

```bash
jupyter notebook backend/rag_pipeline.ipynb
```

### Frontend

```bash
streamlit run frontend/app.py
```

The app opens at `http://localhost:8501`.

---

## 📦 Requirements

Example `requirements.txt` (adjust to match your environment):

```
streamlit
langchain
langchain-community
langchain-groq
langchain-huggingface
sentence-transformers
faiss-cpu
pypdf
python-dotenv
jupyter
```

---

## 🧠 RAG Pipeline Details

| Stage | Component | Notes |
|---|---|---|
| Loading | `PyPDFLoader` | Keeps page metadata for citations |
| Chunking | `RecursiveCharacterTextSplitter` | e.g. `chunk_size=1000`, `chunk_overlap=200` |
| Embeddings | HuggingFace Embeddings | e.g. `sentence-transformers/all-MiniLM-L6-v2` |
| Vector store | `FAISS` | Local, fast similarity search |
| Retrieval | `as_retriever()` | e.g. `k=3` most relevant chunks |
| Prompting | `PromptTemplate` | Instructs the LLM to answer only from context |
| Generation | `ChatGroq` | Produces the final answer |

> Update the values above to match what you used in your notebook.

### Example prompt template

```
You are a helpful assistant for company employees.
Answer the question using ONLY the context below.
If the answer is not in the context, say "I could not find this in the document."

Context:
{context}

Question:
{question}

Answer:
```

---

## 💡 Example Questions

Using an employee handbook as the knowledge base:

- *How many days of annual leave are employees entitled to?*
- *What is the process for reporting a workplace grievance?*
- *What does the code of conduct say about conflicts of interest?*
- *What are the onboarding steps for a new employee?*

---

## 🚀 Key Benefits

- ✅ Upload any company document (PDF)
- ✅ AI reads and understands the document
- ✅ Finds precise answers using semantic search
- ✅ Shows source information and page numbers
- ✅ Saves time and improves productivity

---

## 🔮 Future Improvements

- Support multiple PDFs and other formats (DOCX, TXT)
- Persist the FAISS index to disk to avoid reprocessing
- Add chat history and follow-up questions
- Add user authentication and role-based document access
- Deploy on Streamlit Community Cloud or Docker

---

## 👤 Author

**Your Name**
AI Engineer, Alpha IT Managed Services (Industry Assessment Project)

---

## 📝 License

This project was developed as part of an industry assessment for educational purposes.
