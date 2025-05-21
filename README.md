
# 🔍 RAGNETIC: Multi-PDF RAG Pipeline using LangChain + Mistral + Weaviate

## 🧠 Overview
RAGNETIC is a Retrieval-Augmented Generation (RAG) pipeline that lets you ask natural language questions over multiple PDF documents. It uses:
- **LangChain** for chaining steps
- **Weaviate** as a vector database
- **Mistral-7B** as the local LLM (via Hugging Face Transformers)
- **SentenceTransformers** to embed PDF chunks

---

## 📦 Features
- Load and process multiple PDFs
- Embed and index documents in Weaviate
- Perform semantic search + generate contextual answers
- Uses local models (no OpenAI key needed)

---

## 🧪 Setup

### 1. Install dependencies

```bash
pip install langchain langchain-community langchain-core weaviate-client sentence-transformers transformers accelerate pypdf
```

### 2. Download your Hugging Face model (e.g. Mistral)

```python
from transformers import AutoTokenizer, AutoModelForCausalLM
tokenizer = AutoTokenizer.from_pretrained("mistralai/Mistral-7B-Instruct-v0.3")
model = AutoModelForCausalLM.from_pretrained("mistralai/Mistral-7B-Instruct-v0.3")
```

---

## 📁 How to Use with Multiple PDFs

1. Put all your PDFs in a folder (e.g. `./docs`)
2. Modify the ingestion step like this:

```python
from langchain.document_loaders import PyPDFLoader

pdf_folder = "./docs"
all_docs = []

for file in Path(pdf_folder).glob("*.pdf"):
    loader = PyPDFLoader(str(file))
    docs = loader.load()
    all_docs.extend(docs)
```

Now you have all PDFs combined in `all_docs`, and can split, embed, and store them the same way.

---

## 🧠 Ask Questions

```python
query = "What is forecasting?"
answer = rag_chain.invoke(query)
print(answer)
```

---

## ✅ To-Do
- Add metadata filtering
- Show document sources
- Add streaming output

---

## 👤 Author
RAGNETIC – Powered by LangChain, Mistral, and awesome open-source tools.
