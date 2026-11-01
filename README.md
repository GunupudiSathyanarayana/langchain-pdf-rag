# LangChain Document Retrieval

This project demonstrates document retrieval and retrieval-augmented generation (RAG) with LangChain. The notebook loads a local PDF, indexes its text with FAISS, retrieves relevant passages for a question, and passes those passages to a local Ollama language model to generate an answer.

## What the notebook does

[`retriever.ipynb`](./retriever.ipynb) walks through these steps:

1. Loads `attention.pdf` with LangChain's PDF loader.
2. Splits the PDF into chunks of up to 1,000 characters, with 200 characters of overlap.
3. Creates OpenAI embeddings for the first 30 chunks and stores them in an in-memory FAISS index.
4. Runs a similarity search and displays a matching passage.
5. Creates a retriever and a LangChain retrieval chain.
6. Sends the retrieved context and question to the local Ollama `llama2` model and displays its answer.

The notebook uses OpenAI for embeddings and Ollama for text generation. OpenAI API usage may incur charges. The FAISS index is created in memory each time the notebook runs.

## Project files

- `retriever.ipynb` — the retrieval and RAG walkthrough.
- `attention.pdf` — the PDF indexed by the notebook.
- `requirements.txt` — Python package dependencies.
- `.env` — local environment variables, including the OpenAI API key; keep this file private.

## Run locally

### Prerequisites

- Python installed.
- An OpenAI API key for the embedding requests.
- [Ollama](https://ollama.com/) installed and running locally, with the `llama2` model available.
- A notebook environment, such as the Jupyter extension in Visual Studio Code.

### 1. Create a virtual environment and install dependencies

**Windows PowerShell**

```powershell
py -m venv .venv
.\.venv\Scripts\Activate.ps1
python -m pip install --upgrade pip
python -m pip install -r requirements.txt
```

If PowerShell prevents activation, run the install commands directly with the environment's Python:

```powershell
.\.venv\Scripts\python.exe -m pip install --upgrade pip
.\.venv\Scripts\python.exe -m pip install -r requirements.txt
```

**macOS / Linux**

```bash
python3 -m venv .venv
source .venv/bin/activate
python -m pip install --upgrade pip
python -m pip install -r requirements.txt
```

### 2. Configure OpenAI

Create a `.env` file in the project directory:

```dotenv
OPENAI_API_KEY=your_openai_api_key
```

Replace the example value with your key. Do not commit or share the real key.

### 3. Prepare Ollama

Start Ollama, then download the model used by the notebook:

```bash
ollama pull llama2
```

### 4. Run the notebook

Open `retriever.ipynb` in Visual Studio Code with the Jupyter extension (or another Jupyter environment) and select the project's virtual environment as its Python kernel. Run the cells from top to bottom with the project directory as the working directory so the notebook can find `attention.pdf`.
