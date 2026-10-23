# Local Chatbot with LangChain, Ollama and Streamlit

A simple Streamlit app that answers questions using a local **Gemma 2B** model served by Ollama. It uses a LangChain chain (`prompt | llm | output_parser`). No OpenAI key is needed.

## Features

- Runs fully on your machine with Ollama
- LangChain prompt template and output parser
- Simple Streamlit web interface
- Optional LangSmith tracing

## Prerequisites

- Python 3.10+
- [Ollama](https://ollama.com/download) installed and running

## Setup

1. **Clone the repo**

   ```bash
   git clone https://github.com/<your-username>/<your-repo>.git
   cd <your-repo>
   ```

2. **Create and activate an environment**

   ```bash
   python -m venv venv
   source venv/bin/activate
   ```

   Or with conda:

   ```bash
   conda create -p ./venv python=3.10 -y
   conda activate ./venv
   ```

3. **Install dependencies**

   ```bash
   pip install -r requirements.txt
   ```

4. **Pull the model**

   ```bash
   ollama pull gemma:2b
   ```

   Make sure Ollama is running (open the Ollama app, or run `ollama serve`).

5. **(Optional) Enable LangSmith tracing**

   ```bash
   cp .env.example .env
   ```

   Add your LangSmith API key to `.env`. Skip this step if you don't need tracing.

## Run

```bash
streamlit run simpleapp.py
```

Open http://localhost:8501 and type a question.

## How It Works

```python
chain = prompt | llm | output_parser
```

1. `ChatPromptTemplate` wraps your question with a system instruction
2. `OllamaLLM` (`gemma:2b`) generates the answer locally
3. `StrOutputParser` returns plain text, which Streamlit displays

## Troubleshooting

| Problem | Fix |
|---|---|
| `command not found: streamlit` | Activate your environment and run `pip install -r requirements.txt` |
| `ModuleNotFoundError: langchain_ollama` | Run `pip install langchain-ollama` in the active environment |
| Connection refused / `ConnectError` | Ollama isn't running. Open the app or run `ollama serve` |
| Model not found | Run `ollama pull gemma:2b` |

## Tech Stack

LangChain, Ollama, Streamlit

## License

MIT
