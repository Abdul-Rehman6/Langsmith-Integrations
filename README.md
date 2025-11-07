# 🚀 LangSmith Integrations Showcase: Observability for LLM Architectures

[![Python](https://img.shields.io/badge/Python-3.10%2B-blue)](https://www.python.org/)
[![Framework](https://img.shields.io/badge/Framework-LangChain-brightgreen)](https://www.langchain.com/)
[![Tracing](https://img.shields.io/badge/Tracing-LangSmith-F87A7A)](https://www.langchain.com/langsmith)
[![License](https://img.shields.io/badge/License-MIT-yellow)](https://opensource.org/licenses/MIT)
[![Open Issues](https://img.shields.io/github/issues/Abdul-Rehman6/Langsmith-Integrations)](https://github.com/Abdul-Rehman6/Langsmith-Integrations/issues)

## 🌟 Project Overview

This repository is dedicated to demonstrating how to effectively instrument, trace, and debug various **Large Language Model (LLM) application architectures** using **LangSmith**.

Developing reliable LLM applications requires visibility into the complex internal steps—the chains, agents, tools, and retrievers. LangSmith provides this essential observability.

This showcase features a set of progressively complex examples, from basic single calls to advanced, stateful LangGraph workflows, ensuring every component's execution is fully tracked, allowing for performance optimization and debugging of runtime failures.

---

## ✨ Integrations & Key Concepts Demonstrated

The power of LangSmith lies in its ability to provide granular visibility into the most common LLM patterns. The following table details the examples included and the core concept each one illustrates in LangSmith.

| File | Integration Type | LangSmith Trace Focus | Concept Explained |
| :--- | :--- | :--- | :--- |
| `1_simple_llm_call.py` | **Basic Invocation** | `llm_call` span | The foundation of tracing: logging a single input, model configuration, and output/latency. |
| `2_sequential_chain.py` | **Sequential Chain** | Multiple sequential `chain` spans | Tracing a fixed, linear pipeline. Shows how output from one step (e.g., summarization) becomes input for the next (e.g., translation). |
| `3_rag.py` | **Retrieval-Augmented Generation (RAG)** | `retriever` and `llm_call` spans | The most critical pattern: viewing the documents retrieved (`source nodes`) before the LLM generates the final answer. Essential for hallucination debugging. |
| `4_agent.py` | **Autonomous Agent** | `agent` and `tool` spans, `action` loops | Tracing complex, non-linear, decision-making cycles. Shows the Agent's thought process (the "scratchpad") and how it decides to use various tools. |
| `5_langgraph.py` | **LangGraph Workflow** | `graph` and `node` spans, conditional transitions | Observability for advanced stateful applications. Traces state changes, conditional routing, and cycles (loops) within the workflow structure. |

---

## 🚀 Getting Started

To explore these examples, you need to set up your environment with the necessary keys and dependencies.

### Prerequisites

* **Python 3.10+**
* **OpenAI API Key** (Required for the `langchain-openai` integration)
* **LangSmith API Key** (Obtain one by signing up for the [LangSmith platform](https://www.langchain.com/langsmith))

### Installation Steps

1.  **Clone the Repository:**

    ```bash
    git clone [https://github.com/Abdul-Rehman6/Langsmith-Integrations.git](https://github.com/Abdul-Rehman6/Langsmith-Integrations.git)
    cd Langsmith-Integrations
    ```

2.  **Create and Activate a Virtual Environment:**

    Using a virtual environment prevents dependency conflicts.

    ```bash
    python -m venv venv
    source venv/bin/activate  # On Linux/macOS
    # .\venv\Scripts\activate  # On Windows
    ```

3.  **Install Dependencies:**

    The `requirements.txt` file contains all necessary packages, including `langchain`, `langchain-openai`, `langgraph`, and `python-dotenv`.

    ```bash
    pip install -r requirements.txt
    ```

---

## 🔑 Configuration (API Keys & Environment Variables)

All examples securely load configuration from a `.env` file using the `python-dotenv` library.

1.  **Create a `.env` file** in the root directory of the project.

2.  **Populate the `.env` file** with your credentials. **Note:** Setting `LANGCHAIN_TRACING_V2="true"` is essential for LangSmith integration.

    ```bash
    # --- LLM Provider Key ---
    # Used by langchain-openai for model calls
    OPENAI_API_KEY="YOUR_OPENAI_API_KEY"

    # --- LangSmith Configuration ---

    # ENABLE LangSmith Tracing
    LANGCHAIN_TRACING_V2="true"

    # Your LangSmith API Key (found in your developer settings)
    LANGCHAIN_API_KEY="YOUR_LANGSMITH_API_KEY"

    # Define the project name where traces will be grouped in the LangSmith UI
    LANGCHAIN_PROJECT="Langsmith-Integrations-Showcase"

    # (Optional) Endpoint for self-hosted instances. Default is the public cloud.
    # LANGCHAIN_ENDPOINT="[https://api.smith.langchain.com](https://api.smith.langchain.com)"
    ```

---

## ▶️ Usage and Debugging

Run any script, and the trace will automatically be sent to your LangSmith project defined in the `.env` file.

```bash
# Example: Run the RAG pipeline
python 3_rag.py
