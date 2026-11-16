# 🔌 Multi-Server MCP Agent — Model Context Protocol

A production-style implementation of Anthropic's **Model Context Protocol (MCP)** connecting multiple heterogeneous tool servers to a ReAct AI agent.

[![Python](https://img.shields.io/badge/Python-3.11+-3776AB?style=flat&logo=python&logoColor=white)](https://python.org)
[![MCP](https://img.shields.io/badge/Protocol-MCP-8A2BE2?style=flat)](https://modelcontextprotocol.io/)
[![Groq](https://img.shields.io/badge/Inference-Groq_LLaMA_3.1-f55036?style=flat)](https://groq.com/)
[![LangGraph](https://img.shields.io/badge/Agent-LangGraph_ReAct-1C3C3C?style=flat)](https://langchain-ai.github.io/langgraph/)

---

## 🏗️ Architecture

```
                      ┌──────────────────────┐
                      │    Groq LLaMA 3.1    │
                      │    (ReAct Agent)     │
                      └──────────┬───────────┘
                                 │
                   ┌─────────────┴─────────────┐
                   │    MultiServerMCPClient   │
                   └─────────────┬─────────────┘
                                 │
                 ┌───────────────┴───────────────┐
                 │                               │
        [stdio Transport]             [Streamable HTTP Transport]
                 │                               │
                 ▼                               ▼
       ┌───────────────────┐           ┌───────────────────┐
       │   mathserver.py   │           │    weather.py     │
       │  (Math Operations)│           │ (Weather Reports) │
       └───────────────────┘           └───────────────────┘
```

---

## 📂 Repository Contents

- **`client.py`**: Initializes `MultiServerMCPClient`, binds stdio (`mathserver.py`) and HTTP (`weather.py`) toolsets, and drives an asynchronous ReAct agent via `ChatGroq`.
- **`mathserver.py`**: Local stdio MCP tool server for high-precision math computations.
- **`weather.py`**: HTTP streamable MCP tool server for location-based weather fetching.

---

## 🚀 Quick Start

```bash
# 1. Install dependencies
pip install -r requirements.txt

# 2. Set your Groq API key
export GROQ_API_KEY="your-groq-api-key"
# On Windows PowerShell: $env:GROQ_API_KEY="your-groq-api-key"

# 3. Start the weather server (in background or separate terminal)
python weather.py

# 4. Run the multi-server client
python client.py
```

---

<sub>Maintained by [Kaushal Sharma](https://github.com/Kaushal-1925)</sub>
