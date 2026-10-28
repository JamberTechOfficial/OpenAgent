# 🤖 Other AI Agents — Comparison & Setup Guide

---

> This guide helps you discover, compare, and choose the right AI agent for your needs — with an interactive decision tree, detailed profiles, and quick-start commands.

---

## 📋 Table of Contents

1. [🌳 Interactive Decision Tree](#-interactive-decision-tree)
2. [📊 Agent Comparison Table](#-agent-comparison-table)
3. [🔍 Detailed Agent Profiles](#-detailed-agent-profiles)
4. [❓ How to Choose: Interactive Questions](#-how-to-choose-interactive-questions)
5. [⚡ Quick Start Commands](#-quick-start-commands)
6. [🆓 Free LLM APIs to Use](#-free-llm-apis-to-use)

---

## 🌳 Interactive Decision Tree

**Start here — What do you want to do?**

```
What do you want to do?
│
├── 💬 Chat with AI via Telegram?
│       └── → Hermes Agent (NousResearch) ✅ ALREADY SET UP
│
├── 💻 Automate coding tasks?
│       └── → OpenDevin / SWE-agent / Aider
│
├── 🤝 Build multi-agent teams?
│       └── → CrewAI / AutoGen / MetaGPT
│
├── 🌐 Browser automation / web tasks?
│       └── → AgentGPT / AutoGPT
│
├── 📄 RAG / document Q&A?
│       └── → LangChain / LlamaIndex
│
├── 🛠️  Build your own custom agent?
│       └── → LangChain / Pydantic AI / AutoGen
│
└── 🚀 All-in-one platform (no code)?
        └── → SuperAGI / AgentGPT
```

---

## 📊 Agent Comparison Table

| Agent | Type | Best For | Free? | Difficulty | Runs Via |
|---|---|---|---|---|---|
| ✅ **Hermes (NousResearch)** | Personal assistant | Telegram bot, daily tasks | ✅ Yes (NVIDIA API) | 🟡 Medium | Terminal / Telegram |
| **AutoGPT** | Auto task agent | Web search, file tasks | ✅ Yes | 🟡 Medium | Browser / Terminal |
| **AgentGPT** | Web-based | Quick tasks, no install | ✅ Yes (limited) | 🟢 Easy | Browser |
| **SuperAGI** | Multi-agent platform | Complex automation | ✅ Yes (self-host) | 🔴 Hard | Web UI |
| **CrewAI** | Multi-agent team | Role-based workflows | ✅ Yes | 🟡 Medium | Python |
| **AutoGen** | Multi-agent | Research, coding teams | ✅ Yes | 🟠 Medium-Hard | Python |
| **MetaGPT** | Software company sim | Build software with AI team | ✅ Yes | 🔴 Hard | Python |
| **LangChain Agents** | Framework | Build custom agents | ✅ Yes | 🔴 Hard | Python |
| **OpenDevin** | Coding agent | Autonomous software dev | ✅ Yes | 🔴 Hard | Docker |
| **SWE-agent** | Coding agent | Fix GitHub issues | ✅ Yes | 🔴 Hard | Terminal |
| **Pydantic AI** | Framework | Type-safe agents in Python | ✅ Yes | 🔴 Hard | Python |
| **Aider** | Coding assistant | AI pair programmer | ✅ Yes | 🟢 Easy | Terminal |
| **ChatDev** | Multi-agent | Simulated dev team | ✅ Yes | 🟡 Medium | Python |

---

## 🔍 Detailed Agent Profiles

---

### ✅ Hermes Agent (NousResearch) — ALREADY SET UP

- **What it is:** A personal AI agent that lives in your terminal and Telegram — already configured for this community!
- **Why use it:** Free with NVIDIA NIM API, runs 24/7 on a free server, completely private
- **Model:** `NousResearch/Hermes-3-Llama-3.1-70B` — powerful, instruction-following LLM
- **How to set up:** See [`03-hermes-agent-setup.md`](./03-hermes-agent-setup.md)
- **Best for:** Individuals wanting a personal AI assistant accessible anytime via Telegram
- **GitHub:** https://github.com/NousResearch/hermes-agent

### 🤖 AutoGPT

- **What it is:** The pioneering "auto-agent" that runs tasks autonomously — searches web, writes files, executes code
- **Why use it:** Good for complex multi-step tasks, massive community and plugin ecosystem
- **Limitations:** Can go in loops, expensive with GPT-4 API, not ideal for Telegram
- **How to run:** Docker or local Python install
- **Cost:** Requires OpenAI API key (paid) or compatible free API (NVIDIA NIM works!)
- **GitHub:** https://github.com/Significant-Gravitas/AutoGPT
- **Best for:** Power users who want AI to do complex tasks autonomously

### 🌐 AgentGPT

- **What it is:** A web browser-based agent — zero installation required
- **Why use it:** No setup at all, good for quick experiments and demos
- **Limitations:** Browser-only, cannot run 24/7, data privacy concerns with cloud
- **How to use:** Go to https://agentgpt.reworkd.ai → type a goal → watch it run
- **Cost:** Free with usage limits, paid plans for more
- **Best for:** Beginners, quick demos, non-technical users

### 🏢 SuperAGI

- **What it is:** A self-hosted multi-agent platform with a beautiful web dashboard
- **Why use it:** Manage multiple agents, tool integrations, beautiful UI, team use
- **Limitations:** Requires a good server (4+ GB RAM), complex initial setup
- **How to run:** Docker Compose on your VPS/server
- **GitHub:** https://github.com/TransformerOptimus/SuperAGI
- **Best for:** Teams wanting a managed, visual AI agent platform

### 👥 CrewAI

- **What it is:** A framework for building teams of AI agents — each with a specific role
- **Why use it:** Agents can have roles like Researcher, Writer, Analyst and work together in sequence
- **Example workflow:**
  ```
  Research Agent → finds information
       ↓
  Writer Agent → writes the article
       ↓
  Editor Agent → reviews and polishes
  ```
- **How to run:** `pip install crewai` + Python script
- **GitHub:** https://github.com/crewAIInc/crewAI
- **Best for:** Developers building multi-agent, role-based workflows

### 🔬 AutoGen (Microsoft)

- **What it is:** Microsoft's powerful multi-agent conversation framework
- **Why use it:** Agents can have conversations with each other, very flexible orchestration
- **How to run:** `pip install pyautogen` + Python
- **GitHub:** https://github.com/microsoft/autogen
- **Best for:** Research tasks, complex agent systems, coding agent teams

### 🏗️ MetaGPT

- **What it is:** Simulates an entire software company using AI agents for each role
- **Roles included:** Product Manager 📋, Architect 🏛️, Engineer 👨‍💻, QA Tester 🧪
- **How it works:** Give it a requirement → it builds the full software project
- **GitHub:** https://github.com/geekan/MetaGPT
- **Best for:** Generating entire software projects from a single requirement prompt

### 🔗 LangChain Agents

- **What it is:** The most popular and flexible agent framework in the AI ecosystem
- **Why use it:** Massive ecosystem, tools for RAG, memory, chains, and custom agent logic
- **How to run:** `pip install langchain` + Python
- **Docs:** https://docs.langchain.com
- **Best for:** Developers who need full control to build custom agents with diverse tools

### 🖥️ OpenDevin

- **What it is:** An autonomous AI software developer that can write, run, and debug code
- **Capabilities:** Writes code ✏️, runs tests 🧪, browses web 🌐, fixes bugs 🐛
- **Requirements:** Docker installed, 8+ GB RAM recommended
- **GitHub:** https://github.com/OpenDevin/OpenDevin
- **Best for:** Developers who want AI to autonomously develop software end-to-end

### 🧑‍💻 Aider

- **What it is:** An AI pair programmer that works right inside your terminal
- **How to use:** Run `aider` in your code directory → ask it to add/fix/change code in plain English
- **Why use it:** Extremely practical, works with any existing codebase, supports many LLMs (including free ones!)
- **GitHub:** https://github.com/paul-gauthier/aider
- **Best for:** Developers who want hands-on AI assistance with real coding day-to-day

## ❓ How to Choose: Interactive Questions

Work through these questions to find your perfect agent:

```
Q1: Do you want to use AI WITHOUT writing any code?
    ├── YES → AgentGPT (browser, zero install)
    │          or SuperAGI (web UI, needs a server)
    └── NO  → Go to Q2 ↓

Q2: Do you want to access it via Telegram?
    ├── YES → ✅ Hermes Agent — already set up for you!
    │          (See 03-hermes-agent-setup.md)
    └── NO  → Go to Q3 ↓

Q3: Is your main goal coding / software development?
    ├── YES → Aider       (easy, day-to-day coding help)
    │          OpenDevin  (autonomous, full dev cycle)
    │          SWE-agent  (fixing GitHub issues)
    └── NO  → Go to Q4 ↓

Q4: Do you want multiple AI agents working as a TEAM?
    ├── YES → CrewAI     (easiest team setup)
    │          AutoGen    (most flexible)
    │          MetaGPT    (builds entire software projects)
    └── NO  → Go to Q5 ↓

Q5: Do you want to BUILD your own custom agent?
    ├── YES → LangChain Agents (most ecosystem)
    │          Pydantic AI     (type-safe, clean Python)
    │          AutoGen         (conversational agents)
    └── NO  → Hermes Agent or LangChain for general use ✅
```

---

## ⚡ Quick Start Commands

### Setup Commands for Each Agent

> **Note:** For all agents requiring an API key, you can use the free NVIDIA NIM API from https://build.nvidia.com as a drop-in OpenAI-compatible endpoint.

---

#### ✅ Hermes Agent (Already Set Up!)
```bash
# Already configured — just run:
cd ~/hermes-agent
python agent.py
# Then message your Telegram bot!
```

---

#### 🤖 AutoGPT
```bash
# Option 1: Docker (recommended)
git clone https://github.com/Significant-Gravitas/AutoGPT.git
cd AutoGPT
cp .env.template .env
# Edit .env and add your API key
docker compose run --rm auto-gpt

# Option 2: Local Python
pip install auto-gpt
```

---

#### 🌐 AgentGPT
```bash
# No installation needed!
# Just open your browser and go to:
# https://agentgpt.reworkd.ai
# Type your goal and hit Run!
```

---

#### 🏢 SuperAGI
```bash
git clone https://github.com/TransformerOptimus/SuperAGI.git
cd SuperAGI
cp config_template.yaml config.yaml
# Edit config.yaml with your API keys
docker compose up --build -d
# Then open: http://localhost:3000
```

---

#### 👥 CrewAI
```bash
pip install crewai crewai-tools

# Create a simple crew:
python -c "
from crewai import Agent, Task, Crew

researcher = Agent(role='Researcher', goal='Find information', backstory='Expert researcher')
writer = Agent(role='Writer', goal='Write articles', backstory='Professional writer')

task = Task(description='Research AI agents and write a summary', agent=researcher)
crew = Crew(agents=[researcher, writer], tasks=[task])
result = crew.kickoff()
print(result)
"
```

---

#### 🔬 AutoGen (Microsoft)
```bash
pip install pyautogen

python -c "
import autogen
config_list = [{'model': 'gpt-4', 'api_key': 'YOUR_KEY'}]
assistant = autogen.AssistantAgent('assistant', llm_config={'config_list': config_list})
user_proxy = autogen.UserProxyAgent('user_proxy', code_execution_config={'work_dir': 'coding'})
user_proxy.initiate_chat(assistant, message='Write a Python function to sort a list')
"
```

---

#### 🏗️ MetaGPT
```bash
pip install metagpt

# Run MetaGPT to build a software project:
metagpt "Create a Python todo list application with a REST API"
```

---

#### 🔗 LangChain Agents
```bash
pip install langchain langchain-openai langchain-community

python -c "
from langchain.agents import AgentType, initialize_agent, load_tools
from langchain.llms import OpenAI

llm = OpenAI(temperature=0)
tools = load_tools(['wikipedia', 'llm-math'], llm=llm)
agent = initialize_agent(tools, llm, agent=AgentType.ZERO_SHOT_REACT_DESCRIPTION, verbose=True)
agent.run('What is the population of Pakistan and what is it squared?')
"
```

---

#### 🖥️ OpenDevin
```bash
# Requires Docker Desktop installed first!
docker pull ghcr.io/opendevin/sandbox:latest

docker run -it \
    -e LLM_API_KEY="your-api-key" \
    -e LLM_MODEL="gpt-4" \
    -v /var/run/docker.sock:/var/run/docker.sock \
    -p 3000:3000 \
    ghcr.io/opendevin/opendevin:latest

# Open: http://localhost:3000
```

---

#### 🧑‍💻 Aider
```bash
pip install aider-chat

# Navigate to your project directory:
cd your-project-folder

# Start Aider with your preferred model:
aider --model gpt-4                          # OpenAI GPT-4
aider --openai-api-base https://integrate.api.nvidia.com/v1  # NVIDIA NIM (free!)
aider --model ollama/codellama               # Local Ollama (completely free!)

# Then just type what you want to change in plain English!
```

---

#### 💬 ChatDev
```bash
git clone https://github.com/OpenBMB/ChatDev.git
cd ChatDev
pip install -r requirements.txt

python run.py \
    --task "Build a simple calculator application" \
    --name "CalculatorApp" \
    --model "gpt-4"
```

---

## 🆓 Free LLM APIs to Use

Most agents need an LLM API. Here are the best **free** options:

| API Provider | Free Tier Details | Best Used With | Sign Up |
|---|---|---|---|
| 🟢 **NVIDIA NIM** | Very generous free credits | Hermes, ANY OpenAI-compatible agent | https://build.nvidia.com |
| 🟢 **Groq** | Free tier, blazing fast inference | Aider, LangChain, CrewAI | https://console.groq.com |
| 🟡 **OpenRouter** | Mix of free & paid models | Any agent with OpenAI-compatible API | https://openrouter.ai |
| 🟢 **Google Gemini API** | Free tier available | LangChain, AutoGen | https://ai.google.dev |
| 🟡 **Together AI** | \$25 free credit on signup | Most Python frameworks | https://api.together.xyz |
| 🟢 **Ollama** | 100% Free — runs locally | Aider, LangChain, any local agent | https://ollama.ai |
| 🟡 **Hugging Face** | Free Inference API | Research, LangChain | https://huggingface.co |

> **💡 Tip:** Start with **NVIDIA NIM** (best free tier) or **Ollama** (completely local, no API key needed). Hermes Agent is already configured with NVIDIA NIM!

---

## 🗺️ Quick Reference Summary

| I want to... | Use this agent | Difficulty |
|---|---|---|
| Chat via Telegram right now | ✅ Hermes Agent | Already done! |
| Try AI in the browser instantly | AgentGPT | 🟢 Easy |
| Get coding help in my terminal | Aider | 🟢 Easy |
| Build a role-based AI team | CrewAI | 🟡 Medium |
| Let AI write entire software | MetaGPT / OpenDevin | 🔴 Hard |
| Build a custom agent framework | LangChain / AutoGen | 🔴 Hard |
| Self-host a full AI platform | SuperAGI | 🔴 Hard |

---

## 📚 Related Documentation

- 📄 [`01-what-is-hermes.md`](./01-what-is-hermes.md) — What is the Hermes model?
- 📄 [`02-nvidia-nim-setup.md`](./02-nvidia-nim-setup.md) — Setting up the NVIDIA NIM API
- 📄 [`03-hermes-agent-setup.md`](./03-hermes-agent-setup.md) — Full Hermes Agent setup guide
- 📄 [`05-free-llm-apis.md`](./05-free-llm-apis.md) — More free API options

---

*Last updated: 2025 | Maintained by the JT Community | Always keep learning* 🚀
