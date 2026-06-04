# 🎙️ NewsTeller: An Autonomous Agentic AI Journalist Network

NewsTeller is a fully decoupled, multi-stream data ingestion and audio synthesis platform that transforms a traditional web scraper into a live, autonomous digital newsroom. By combining **deterministic traditional web crawling** with an **autonomous Model Context Protocol (MCP) LangGraph AI Agent**, the application functions as a complete virtual news channel. 

The system independently scopes out targeted topics, bypasses modern web firewalls, aggregates public sentiment, synthesizes broadcast-ready audio scripts via Large Language Models (LLMs), and converts them into studio-grade vocal audio files.

---

## 🏗️ Architecture & Core Components Overview

NewsTeller uses a decoupled **Client-Server (Frontend-Backend) Architecture**. This ensures that the user interface is completely separate from the heavy, resource-intensive scraping and AI logic.

```markdown
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


### 1. The Client UI (`frontend.py`)
Built with **Streamlit**, this acts as the user control panel. It records custom topics, maintains user choices dynamically in system memory using session states, structures configuration requests into standard JSON payloads, and sends them to the server. It handles the incoming audio binary data stream to render an native HTML5 media player and a download portal.

### 2. The Data Gatekeeper (`models.py`)
Built with **Pydantic**, this file guarantees system stability. It enforces strict structural rules (`NewsRequest`) on incoming data payloads before they hit the server engine. If a payload contains structural errors or missing parameters, it is caught and rejected immediately.

### 3. The Air Traffic Controller (`backend.py`)
Built with **FastAPI**, this asynchronous server coordinates your workflows. It runs continuously on your network, handles incoming data requests on a custom port (`1111`), parallelizes data-fetching workers, routes aggregated texts to the AI synthesizer, and streams raw audio binary bytes (`audio/mpeg`) back to the client interface.

### 4. The Specialized Factory Floor (`utils.py`)
The architectural foundation of your system's utilities. It houses explicit functions responsible for URL string sanitization (`quote_plus`), HTML scraping and cleaning (`BeautifulSoup`), local AI execution models (`Ollama/Llama 3.2`), target script formatting templates (**Claude 3 Opus**), and premium audio conversion pipelines (**ElevenLabs / gTTS**).

---

## 🤖 The Data Ingestion Engine: Deterministic vs. Agentic

The true technical innovation of NewsTeller is its **hybrid data ingestion architecture**, dividing research duties into two distinct strategies:

### 🌐 Traditional News Ingestion (`News_scraper.py`)
The traditional media crawler is fully **deterministic**. It executes explicit, step-by-step instructions:
1. Translates a phrase into a pre-sorted chronological Google News URL.
2. Forwards the query directly to **Bright Data’s Web Unlocker API** to solve CAPTCHAs, rotate IP addresses, and bypass anti-bot scrapers (like Cloudflare).
3. Uses `BeautifulSoup` to strip away messy page elements and isolate clear text.
4. Uses keyword anchor logic (`More`) to reliably extract live news headlines.

### 📑 The Agentic Journalist (`Reddit_scraper.py`)
The social media tracker functions as an **Autonomous Agentic Journalist**. Instead of following rigid scraping scripts, it acts like an open-ended investigative researcher:
1. **Model Context Protocol (MCP):** It spawns an external Node.js subprocess process running the official `@brightdata/mcp` protocol. This lets the AI agent dynamically discover its own active browser and scraping tools at runtime.
2. **LangGraph ReAct Loop:** It configures an autonomous **Reasoning & Action (ReAct)** assistant using Claude 3.5 Sonnet. 
3. **Critical Synthesis:** The agent reads your raw instructions, decides which search tools to utilize, extracts target forum comments, enforces strict constraints (filtering out anything older than a rolling 14-day window), evaluates public sentiment, and structures anonymized narrative quotes.

---

## 📡 End-to-End Data Lifecycle

1. **Input:** The user inputs a topic (e.g., *"Quantum Computing"*) on the Streamlit page and clicks **Generate Summary**.
2. **Request:** The frontend formats this into a JSON payload and transmits it over port `1111` to the FastAPI backend.
3. **Extraction:** The backend calls `NewsScraper` and the `Reddit Agent` to fetch concurrent data packets using your **Bright Data Proxy Architecture**.
4. **Scripting:** The compiled text is aggregated and forwarded to **Claude 3 Opus** with a strict system instruction to write a clean, TTS-friendly, television-style news script without any markdown tags or introductory chatter.
5. **Vocal Forge:** The generated text script is pushed directly to the **ElevenLabs SDK** (with a free native **gTTS** fallback system) to generate a high-fidelity `.mp3` broadcast.
6. **Delivery:** The backend reads the local file as raw bytes and streams it across the network connection, where the frontend converts it into an playable browser widget.



---
FEATURES
- 🗞️ Scrape premium news websites (bypassing paywalls)
- 🕵️♂️ Extract live Reddit reactions (even from JS-heavy threads)
- 🔊 AI-powered audio summaries (text-to-speech with ElevenLabs)
- ⚡ Real-time updates (thanks to Bright Data's MCP magic)

---
PREREQUISITES
- Python 3.9+
- Bright Data account (https://brightdata.com)
- ElevenLabs account (https://elevenlabs.io)

---
QUICK START

1. Clone the Dojo
```
git clone https://github.com/11snigdha11/PERSONAL_AI_JOURNALIST
cd PERSONAL_AI_JOURNALIST
```

2. Install Dependencies
```
pipenv install
pipenv shell
```

3. Environment Setup
Create .env file:
```
cp .env.example .env
```

Configure your secrets in .env:
```
# Bright Data
BRIGHTDATA_MCP_KEY="your_mcp_api_key"
BROWSER_AUTH="your_browser_auth_token"

# ElevenLabs 
ELEVENLABS_API_KEY="your_text_to_speech_key"
```

4. Bright Data Setup
- Create MCP zone: https://brightdata.com/cp/zones
- Enable browser authentication
- Copy credentials to .env

---
RUNNING THE CODE

First terminal (Backend):
```
pipenv run python backend.py
```

Second terminal (Frontend):
```
pipenv run streamlit run frontend.py
```

---
PROJECT STRUCTURE
```
.
├── frontend.py          # Streamlit UI
├── backend.py           # API & data processing  
├── utils.py             # UTILS  
├── news_scraper.py      # News Scraper  
├── reddit_scraper.py    # Reddit Scraper  
├── models.py            # Pydantic model
├── Pipfile              # Dependency scroll
├── .env.example         # Secret map template
└── requirements.txt     # Alternative dependency list
```

---
NOTES
- First scrape takes 15-20 seconds 
- Reddit scraping uses real browser emulation via MCP
- Keep .env file secret

---
SUPPORT

Bright Data support: https://brightdata.com/support
