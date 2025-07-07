
# 🤖 Pull Request Agent for Hugging Face Hub

Welcome to the **Pull Request Agent Project**, developed as part of **Unit 3 of the MCP Course**!

This project demonstrates a real-world integration of the MCP framework to automatically tag Hugging Face model repositories by analyzing discussions and comments. The agent creates pull requests to suggest metadata improvements, helping model authors keep their repositories well-organized with minimal manual effort.

---

## 📌 Overview

You’ll build a production-ready PR agent application that consists of:

- ✅ An **MCP server** to interact with the Hugging Face Hub API  
- ✅ A **FastAPI webhook listener** for receiving discussion events  
- ✅ An **intelligent agent** that analyzes content and suggests tags  
- ✅ **Containerized deployment** to Hugging Face Spaces  

By the end of this project, you’ll have a working webhook-driven application that can monitor model discussions and open automated pull requests to improve tags.

---

## 📚 What You’ll Learn

- Create an MCP Server using `FastMCP`
- Implement secure webhook listeners for Hugging Face discussion events
- Build tagging workflows that respond to comments in real-time
- Deploy your PR agent to Hugging Face Spaces using Docker

---

## 🧠 Prerequisites

Before getting started, make sure you:

- Have completed **Units 1 and 2** of the MCP course or understand the concepts
- Are comfortable with:
  - Python 3.11+
  - FastAPI and webhook event handling
  - Hugging Face Hub workflows and Pull Requests
- Have:
  - A Hugging Face account with API access
  - A development environment set up for Python projects

---

## 🗂 Project Structure

| File             | Purpose                                                                 |
|------------------|-------------------------------------------------------------------------|
| `mcp_server.py`  | Core MCP server to read/update model tags                               |
| `app.py`         | FastAPI webhook listener & tagging agent logic                          |
| `requirements.txt` | Python dependencies (FastAPI, FastMCP, Hugging Face Hub client, etc.) |
| `pyproject.toml` | Project metadata and build configuration (using `uv` or `poetry`)       |
| `Dockerfile`     | Docker container setup for Hugging Face Spaces                          |
| `env.example`    | Template environment variables (secrets, API tokens, etc.)              |
| `cleanup.py`     | Optional utility for cleaning test resources                            |

---

## 🧱 System Architecture

```
[ User creates comment ] 
         ↓
[ Hugging Face Webhook triggers ] 
         ↓
[ FastAPI Listener receives POST request ]
         ↓
[ Agent processes content → detects tags ]
         ↓
[ Pull Request created with tag suggestions ]
```

The webhook is validated for security using shared secrets. Tag detection supports both explicit (`tag: pytorch`) and implicit (`uses PyTorch`) references.

---

## ⚙️ Installation

1. **Clone the repository**

```bash
git https://github.com/samir-aitabbou/Pull-Request-Agent-Project.git
cd pr-agent-huggingface
```

2. **Create and activate a virtual environment**

```bash
python -m venv .venv
source .venv/bin/activate
```

3. **Install dependencies**

```bash
pip install -r requirements.txt
```

4. **Create and configure your `.env` file**

```bash
cp env.example .env
# Edit .env to add your Hugging Face token and webhook secret
```

5. **Run the application locally**

```bash
uvicorn app:app --reload
```

You can test the server using simulated webhook POST requests or via a Gradio test UI.

---

## 🚀 Deployment (on Hugging Face Spaces)

This project is container-ready. To deploy:

1. Push your repo to Hugging Face with a Docker-based Space
2. Ensure your `Dockerfile` installs dependencies and exposes the correct port
3. Set environment variables in the Space settings (matching `.env.example`)
4. Your PR Agent will be live and listening for webhooks!

---

## 🔐 Webhook Security

- Each webhook request is authenticated using a shared secret
- Events are validated before processing to prevent abuse
- Pull request creation happens in the background for fast webhook responses

---

## 🤖 Agent Behavior

The PR agent can:

- Detect explicit tags like `tag: pytorch`, `#transformers`, or `tag:vision`
- Use basic NLP to infer common ML-related tags from natural language
- Validate tag suggestions against a list of known ML/AI categories
- Automatically open pull requests on the Hugging Face Hub with clear PR descriptions

---

