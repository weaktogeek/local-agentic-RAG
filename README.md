# local-agentic-RAG

This project demonstrates a **local AI agent** with **Retrieval-Augmented Generation (RAG)** using [Ollama](https://ollama.ai/), [ChromaDB](https://www.trychroma.com/), and Python.

It combines a **language model** (Llama) with an **embedding model** (mxbai-embed-large) to retrieve relevant information from a dataset and generate contextual responses.

---

## 🚀 Setup Instructions

### 1. Create and activate a virtual environment

```bash
python3 -m venv ./venv
source venv/bin/activate   # MacOS/Linux
.\venv\Scripts\activate    # Windows PowerShell
```

### 2. Install [Ollama](https://ollama.ai/)

Download and install Ollama from their official site.

### 3. Pull required models

We need both a **language model** and an **embedding model**:

```bash
ollama pull llama3.2
ollama pull mxbai-embed-large
```

---

## 🧩 Project Structure

* **`main.py`**

  * Defines the **Llama model** and prompt.
  * Line of interest:

    ```python
    reviews = retriever.invoke(question)
    ```

    This calls the **vector DB** (`vector.py`) and retrieves matching responses.

* **`vector.py`**

  * Uses **ChromaDB** for vector searching.
  * Loads the **mxbai-embed-large** embedding model.
  * Ingests a dataframe created from the provided CSV.
  * Returns the **top 5 matching reviews** based on similarity search.

* **ChromaDB storage**

  * Persisted locally at:

    ```
    ./chrome_langchain_db
    ```
  * Stores embeddings on disk.

---

## ⚙️ How it Works

1. User asks a **question**.
2. `vector.py` searches the ChromaDB index for **similar embeddings**.
3. The **top 5 matches** are returned.
4. `main.py` passes these to the **Llama model** for context-aware response generation.

---

## ✅ Example Workflow

```bash
python main.py
```

* Input: `"What do users think about the app performance?"`
* The agent retrieves **relevant reviews** from ChromaDB.
* Llama model generates a **summarized answer** using retrieved context.

---

## 📂 Requirements

* Python 3.9+
* [Ollama](https://ollama.ai/) installed locally
* [ChromaDB](https://www.trychroma.com/)

Install Python dependencies:

```bash
pip install -r requirements.txt
```

---

## 🔮 Next Steps

* Extend with **custom datasets**.
* Experiment with **different Ollama models**.
* Add **API endpoints** for integration with applications.

---
