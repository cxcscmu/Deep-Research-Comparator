# Deep-Research-Comparator

Official repository for Deep Research Comparator — a platform designed for fine-grained human annotations of deep research agents.

## Demo
[![Watch the demo](https://img.youtube.com/vi/g4d2dnbdseg/hqdefault.jpg)](https://youtu.be/g4d2dnbdseg?si=zEs7qQIKtVYOCoFi)

## Table of Contents
- [Prerequisites](#prerequisites)
- [Backend Setup](#backend-setup)
- [Frontend Setup](#frontend-setup)
- [Configuration](#configuration)
- [Running the Platform](#running-the-platform)

## Prerequisites
- Python 3.12 (Conda recommended for environment isolation)
- Node.js 18+ and npm
- PostgreSQL instance accessible to the backend
- API keys for OpenAI, Serper, Gemini, and Perplexity (depending on enabled agents)

## Backend Setup
Run the following commands from the repository root to install dependencies for the backend and agent services:

```bash
cd backend

# Create and activate the Conda environment
conda create -n deepresearch_comparator python=3.12
conda activate deepresearch_comparator

# Install shared dependencies
pip install -r master_requirements.txt

# Install service-specific dependencies (optional to isolate in dedicated envs)
cd app
pip install -r requirements.txt

cd ../gpt_researcher_server
pip install -r requirements.txt

cd ../perplexity_server
pip install -r requirements.txt

cd ../Simple_DeepResearch_server
pip install -r requirements.txt
```

## Frontend Setup
Install the frontend dependencies:

```bash
cd frontend
npm install
```

## Configuration
Each service loads credentials from a `keys.env` file in its root directory.

- **Main backend (`backend/app`)**
  ```bash
  AWS_ENDPOINT="YOUR_DATABASE_URL"
  DB_NAME="YOUR_DATABASE_NAME"
  DB_USERNAME="YOUR_DATABASE_USERNAME"
  DB_PASSWORD="YOUR_DATABASE_PASSWORD"
  GPT_RESEARCHER_URL="http://localhost:5004/run"
  PERPLEXITY_URL="http://localhost:5005/run"
  BASELINE_URL="http://localhost:5003/run"
  ```

- **Simple DeepResearch (`backend/Simple_DeepResearch_server`)**
  ```bash
  GEMINI_API_KEY="YOUR_GEMINI_API_KEY"
  CLUEWEB_API_KEY = "YOUR_CLUEWEB_API_KEY"
  ```

- **Perplexity DeepResearch (`backend/perplexity_server`)**
  ```bash
  PERPLEXITY_API_KEY="YOUR_PERPLEXITY_API_KEY"
  ```

- **GPT Researcher (`backend/gpt_researcher_server`)**
  ```bash
  export OPENAI_API_KEY="YOUR_OPENAI_API_KEY"
  export SERPER_API_KEY="YOUR_SERPER_API_KEY"
  export RETRIEVER=serper
  ```

## Running the Platform
Use separate terminals to start each component in development mode:

```bash
# Frontend
cd frontend
npm run dev
```

```bash
# Main backend
cd backend/app
python app.py
```

```bash
# GPT Researcher agent
cd backend/gpt_researcher_server
python main.py
```

```bash
# Perplexity agent
cd backend/perplexity_server
python main.py
```

```bash
# Simple DeepResearch agent
cd backend/Simple_DeepResearch_server
python main.py
```

By default, the web application is available at `http://localhost:5173/`.

