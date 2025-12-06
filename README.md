
---

# 📘 **End-to-End RAG Pipeline using ChromaDB, Sentence Transformers & Gemini**

A complete **Retrieval-Augmented Generation (RAG)** pipeline built from scratch using:

* **Python**
* **Sentence Transformers** (Embeddings)
* **ChromaDB** (Vector Store)
* **Custom PDF/Text Loaders**
* **LangChain components**
* **Gemini LLM (Google Generative AI)** for final answer generation

This project loads documents (PDF + TXT), splits text, generates embeddings, stores them in a vector database, retrieves relevant chunks, and uses Gemini to generate accurate answers.

---

## 🚀 **Features**

### ✅ Load Documents

* PDF loader using PyMuPDF & LangChain
* Text file loader
* Directory-based ingestion

### ✅ Preprocessing

* RecursiveCharacterTextSplitter
* Metadata handling
* Chunking

### ✅ Embeddings

* SentenceTransformer (`all-MiniLM-L6-v2`)
* EmbeddingManager class
* High-performance vector generation

### ✅ Vector Store

* ChromaDB persistent storage
* VectorStore class
* ID-based document storage
* Metadata tracking

### ✅ Retrieval

* Custom RAGRetriever
* Cosine similarity search
* Thresholding
* Ranked results

### ✅ LLM Integration

* Gemini model (`gemini-flash-latest` or compatible model)
* Context-aware response generation
* End-to-end RAG pipeline

---

# 📁 **Project Structure**

```
RAG/
│
├── data/
│   ├── pdf/
│   │   ├── Harsha Verse Webdev Sheet.pdf
│   │   └── Ultimate AI Resource Sheet.pdf
│   └── text_files/
│       ├── machine_learning.txt
│       └── python_intro.txt
│
├── notebook/
│   ├── document.ipynb
│   └── pdf_loader.ipynb
│
├── main.py
├── README.md
├── requirement.txt
├── pyproject.toml
├── uv.lock
├── .python-version
└── .gitignore
```

---

# 🔧 **Installation**

### 1️⃣ Clone Repository

```sh
git clone https://github.com/<your-username>/end-to-end-rag-pipeline.git
cd end-to-end-rag-pipeline
```

---

### 2️⃣ Install Dependencies

Use **uv**, pip, or conda.

Using pip:

```sh
pip install -r requirement.txt
```

---

### 3️⃣ Add your Google API key

Create a `.env` file:

```
GOOGLE_API_KEY=your_key_here
```

---

# 🧠 **How it Works (Pipeline Overview)**

### 1️⃣ Load documents

```python
loader = DirectoryLoader("data/pdf", glob="**/*.pdf", loader_cls=PyMuPDFLoader)
docs = loader.load()
```

---

### 2️⃣ Split into chunks

```python
splitter = RecursiveCharacterTextSplitter(chunk_size=1000, chunk_overlap=200)
chunks = splitter.split_documents(docs)
```

---

### 3️⃣ Generate embeddings

```python
embedding_manager = EmbeddingManager()
embeddings = embedding_manager.generate_embeddings([doc.page_content for doc in chunks])
```

---

### 4️⃣ Store in ChromaDB

```python
vectorstore = VectorStore()
vectorstore.add_documents(chunks, embeddings)
```

---

### 5️⃣ Retrieve context

```python
retriever = RAGRetriever(vectorstore, embedding_manager)
results = retriever.retrieve("What is machine learning?")
```

---

### 6️⃣ Generate answer with Gemini

```python
answer = rag_simple_gemini("What is machine learning?", retriever)
print(answer)
```

---

# 🧪 **Example Output**

```
Retrieving documents for query: 'What is machine learning?'
Top K: 3
Generating Embeddings...
Retrieved 3 documents

Machine Learning is a subset of AI where machines learn from data...
```

---

# 📦 **Tech Used**

| Component    | Tool                           |
| ------------ | ------------------------------ |
| Embeddings   | Sentence Transformers          |
| Vector Store | ChromaDB                       |
| LLM          | Gemini (Google Generative AI)  |
| Loader       | LangChain Community            |
| Splitting    | RecursiveCharacterTextSplitter |
| Backend      | Python                         |
| PDF Parsing  | PyMuPDF                        |

---
