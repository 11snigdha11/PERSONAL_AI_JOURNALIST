
# 🎙️ NewsTeller: An Autonomous Agentic AI Journalist Network

NewsTeller is a fully decoupled, multi-stream data ingestion and audio synthesis platform that transforms a traditional web scraper into a live, autonomous digital newsroom. By combining **deterministic traditional web crawling** with an **autonomous Model Context Protocol (MCP) LangGraph AI Agent**, the application functions as a complete virtual news channel. 

The system independently scopes out targeted topics, bypasses modern web firewalls, aggregates public sentiment, synthesizes broadcast-ready audio scripts via Large Language Models (LLMs), and converts them into studio-grade vocal audio files.

---

## 🏗️ Architecture & Core Components Overview

NewsTeller uses a decoupled **Client-Server (Frontend-Backend) Architecture**. This ensures that the user interface is completely separate from the heavy, resource-intensive scraping and AI logic.

```mermaid
graph TD
    A[frontend.py Streamlit] -- "HTTP POST (JSON Payload)" --> B[backend.py FastAPI]
    B -- "Raw Audio (Binary Stream)" --> A
    B --> C[News_scraper.py Standard]
    B --> D[Reddit_scraper.py Agentic]

    subgraph News Pipeline
    C --> C1[Targets Google News Feeds]
    C --> C2[Bright Data Web Unlocker]
    C --> C3[Rules-Based Parser]
    end

    subgraph Agentic Pipeline
    D --> D1[LangGraph ReAct Agent Loop]
    D --> D2[@brightdata/mcp Server]
    D --> D3[Autonomous Critical Sorting]
    end

```

### 1. The Client UI (`frontend.py`)

Built with **Streamlit**, this acts as the user control panel. It records custom topics, maintains user choices dynamically in system memory using session states, structures configuration requests into standard JSON payloads, and sends them to the server. It handles the incoming audio binary data stream to render a native HTML5 media player and a download portal.

### 2. The Data Gatekeeper (`models.py`)

Built with **Pydantic**, this file guarantees system stability. It enforces strict structural rules (`NewsRequest`) on incoming data payloads before they hit the server engine. If a payload contains structural errors or missing parameters, it is caught and rejected immediately.

### 3. The Air Traffic Controller (`backend.py`)

Built with **FastAPI**, this asynchronous server coordinates your workflows. It runs continuously on your network, handles incoming data requests on a custom port (`1111`), parallelizes data-fetching workers, routes aggregated texts to the AI synthesizer, and streams raw audio binary bytes (`audio/mpeg`) back to the client interface.

### 4. The Specialized Factory Floor (`utils.py`)

The architectural foundation of your system's utilities. It houses explicit functions responsible for URL string verification and sanitization (`quote_plus`), HTML scraping and cleaning (`BeautifulSoup`), local AI execution models (`Ollama/Llama 3.2`), target script formatting templates (**Claude 3 Opus**), and premium audio conversion pipelines (**ElevenLabs / gTTS**).

---

## 🤖 The Data Ingestion Engine: Deterministic vs. Agentic

The true technical innovation of NewsTeller is its **hybrid data ingestion architecture**, dividing research duties into two distinct strategies:

### 🌐 Traditional News Ingestion (`News_scraper.py`)

The traditional media crawler is fully **deterministic**. It executes explicit, step-by-step instructions:

1. Translates a phrase into a pre-sorted chronological Google News URL.
2. Forwards the query directly to **Bright Data’s Web Unlocker API** to solve CAPTCHAs, rotate IP addresses, and bypass anti-bot scrapers.
3. Uses `BeautifulSoup` to strip away messy page elements and isolate clear text.
4. Uses keyword anchor logic (`More`) to reliably extract live news headlines.

### 📑 The Agentic Journalist (`Reddit_scraper.py`)

The social media tracker functions as an **Autonomous Agentic Journalist**. Instead of following rigid scraping scripts, it acts like an open-ended investigative researcher using the **ReAct (Reasoning and Action)** framework:

1. **Model Context Protocol (MCP):** It spawns an external Node.js subprocess process running the official `@brightdata/mcp` protocol. This lets the AI agent dynamically discover its own active browser and scraping tools at runtime.
2. **LangGraph ReAct Loop:** It configures an autonomous helper assistant using Claude 3.5 Sonnet to cycle through Thought ➔ Action ➔ Observation patterns.
3. **Critical Synthesis:** The agent reads your raw instructions, decides which search tools to utilize, extracts target forum comments, enforces strict constraints (filtering out anything older than a rolling 14-day window), evaluates public sentiment, and structures anonymized narrative quotes.

---

## 📡 End-To-End Data Lifecycle

1. **Input:** The user inputs a topic (e.g., *"Quantum Computing"*) on the Streamlit page and clicks **Generate Summary**.
2. **Request:** The frontend formats this into a JSON payload and transmits it over port `1111` to the FastAPI backend.
3. **Extraction:** The backend calls `NewsScraper` and the `Reddit Agent` to fetch concurrent data packets using your **Bright Data Proxy Architecture**.
4. **Scripting:** The compiled text is aggregated and forwarded to **Claude 3 Opus** with a strict system instruction to write a clean, TTS-friendly, television-style news script without any markdown tags or introductory chatter.
5. **Vocal Forge:** The generated text script is pushed directly to the **ElevenLabs SDK** (with a free native **gTTS** fallback system) to generate a high-fidelity `.mp3` broadcast.
6. **Delivery:** The backend reads the local file as raw bytes and streams it across the network connection, where the frontend converts it into a playable browser widget.

---

## ✨ Features

* 🗞️ **Scrape Target News Websites:** Target Google News with automated chronological sorting.
* 🕵️‍♂️ **Agentic Data Extraction:** Dynamic, tool-aware Reddit research loops via Model Context Protocol (MCP).
* 🔊 **AI-Powered Audio Summaries:** Studio-grade Text-to-Speech narration via the ElevenLabs SDK.
* 🔄 **Cost-Effective Fallbacks:** Integrated code structures to switch gracefully between Cloud LLMs (Claude) and Local LLMs (Ollama/Llama 3.2), and voice synthesis paths (ElevenLabs vs. gTTS).
* ⚡ **Anti-Block Infrastructure:** Managed rate-limiting (`AsyncLimiter`) and exponential backoff retry cycles (`Tenacity`) powered by Bright Data.

---

## 📋 Prerequisites

* Python 3.10+
* Node.js & npm (Required to execute the underlying MCP proxy connection server)
* Bright Data Account ([https://brightdata.com](https://brightdata.com))
* ElevenLabs Account ([suspicious link removed])

---

## 🚀 Quick Start

### 1. Clone the Project

```bash
git clone [https://github.com/11snigdha11/PERSONAL_AI_JOURNALIST.git](https://github.com/11snigdha11/PERSONAL_AI_JOURNALIST.git)
cd PERSONAL_AI_JOURNALIST

```

### 2. Install Dependencies

This project utilizes `pipenv` for environment separation and dependency control.

```bash
pip install pipenv
pipenv install
pipenv shell

```

### 3. Environment Setup

Create your configuration environment file:

```bash
cp .env.example .env

```

Configure your secure credentials inside the generated `.env` file matching your internal utility variables:

```env
# Server Network Port Settings
OLLAMA_HOST=http://localhost:11434

# LLM Providers Validation Keys
ANTHROPIC_API_KEY="your_anthropic_api_key_here"

# Premium Audio Synthesis Credentials
ELEVEN_API_KEY="your_elevenlabs_api_key_here"

# Bright Data Cloud Proxy & MCP Grid Tokens
BRIGHTDATA_API_KEY="your_brightdata_web_unlocker_api_key_here"
BRIGHTDATA_WEB_UNLOCKER_ZONE="your_web_unlocker_zone_name_here"

# MCP Process Interface Authentication Tokens
API_TOKEN="your_brightdata_api_key_here"
WEB_UNLOCKER_ZONE="your_web_unlocker_zone_name_here"

```

---

## 🏃 Running the Infrastructure

To launch the Agentic Newsroom, run both systems inside individual terminal sessions:

**Terminal 1 (Backend Server Platform):**

```bash
pipenv run python backend.py

```

*The FastAPI web routing engine will initialize and boot up hot-reloading protocols on `http://localhost:1111`.*

**Terminal 2 (Frontend User Interface Client):**

```bash
pipenv run streamlit run frontend.py

```

*This mounts the layout dashboard on your local loopback network and automatically reveals the web window at `http://localhost:8501`.*

---

## 📁 Project Architecture Map

```text
.
├── frontend.py        # Streamlit graphical UI & media playback controller
├── backend.py         # FastAPI API endpoints coordinator & async pipeline router
├── utils.py           # Core factory tools: html parsing, text synthesis & audio forging
├── News_scraper.py    # Deterministic Google News web crawler loop
├── Reddit_scraper.py  # Agentic LangGraph AI Journalist powered by Bright Data MCP 
├── models.py          # Pydantic data schemas & verification validations
├── Pipfile            # Project dependencies version tracker
├── .gitignore         # Safety layer to prevent committing credentials & variables
└── .env.example       # Blueprint configuration environmental guide template

```

---

## 💡 Engineering Notes & Support

* **Initial Processing Times:** The initial scrape execution path might require up to 15-20 seconds to compile while the headless browser engines complete protocol handshakes.
* **Data Security:** Never commit your actual `.env` file variables to Git repositories.
* **Bright Data Support:** Review tool configurations and console logs via the [Bright Data Control Center](https://brightdata.com/support).

```


```