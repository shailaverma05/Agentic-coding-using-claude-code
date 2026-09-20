# Claude Code Setup & Workflow

## Overview
A guide to setting up Anthropic's Claude Code CLI, integrating terminal commands into AI context, onboarding to existing codebases, and exploring free local execution alternatives.

---

## 1. Official Anthropic Setup
* **Nature of the Tool:** Claude Code is an agentic, terminal-based CLI coding assistant created by Anthropic.
* **Subscription Tier:** Officially runs via Anthropic's subscription/API tier using frontier models (**Claude 3.7 Sonnet / Opus**).
* **Initial Launch:** 
  * Installed globally via the command line.
  * Prompts directory authorization (trusting files in the folder) on first boot.
  * Authenticates via browser handshake with your Anthropic account.

---

## 2. Project Architecture & Bash Mode
* **Industry Simulation:** Starting with an existing starter skeleton (*Spendly* — a Flask-based expense tracker) mimics real-world software engineering where developers extend legacy or pre-existing codebases rather than building from an empty canvas.
* **Environment Isolation:** Relies on Python virtual environments (`venv`) to keep dependencies isolated.
* **In-Session Bash Mode (`!` / `Shift + 1`):**
  * Allows running shell commands directly inside the Claude CLI prompt.
  * **Core Advantage:** Running commands within the agent automatically appends command execution, outputs, and system errors into Claude’s active context window, enabling contextual debugging and question-answering.

---

## 3. Codebase Onboarding Pattern
When introducing Claude Code to any codebase, run three baseline queries to build model context:
1. **Purpose & Scope:** *"What does this project do?"* — High-level functional breakdown and current implementation status.
2. **Tech Stack Discovery:** *"What tech stack does this project use?"* — Frameworks, template engines, database layers, and testing libraries.
3. **Architecture Mapping:** *"Explain the project structure to me."* — Hierarchical tree layout, component modularity, and key design decisions.

---

## 4. Free Workarounds via Ollama
For running Claude Code without Anthropic API/subscription costs:

### A. Ollama Cloud Mode
* **Command:** `ollama launch claude`
* **Models:** Uses cloud-hosted open models (e.g., *Qwen 3.5*, *GLM*).
* **Trade-off:** No local GPU overhead, but bound by session and weekly free-tier quotas.

### B. Fully Local Offline Models
* **Workflow:** Pull dedicated coding weights locally (e.g., `ollama pull qwen2.5-coder:7b`) and select the local model in `ollama launch claude`.
* **Trade-off:** 100% free with unlimited local usage, but bounded by local RAM/VRAM constraints and slower inference speeds.

---

## Standalone Mindmap

```mermaid
mindmap
  root((Claude Code Setup & Workflow))
    Official Route
      Anthropic Pro / API
      Proprietary Opus & Sonnet
      CLI Global Install
      Browser Auth & Folder Trust
    Environment & Bash Integration
      Starter Skeleton Pattern
      Virtual Environment Isolation
      In-CLI Bash Mode (Shift+1)
        Terminal outputs in LLM context
        Context-aware shell debugging
    Onboarding Discovery Prompts
      Functional Purpose
      Tech Stack Identification
      Architecture & Directory Layout
    Free Tier via Ollama
      ollama launch claude
      Ollama Cloud
        Hosted open models (Qwen 3.5)
        Session quotas apply
      Local Offline Models
        Local download (Qwen 2.5 Coder)
        Zero cost & offline
        Hardware & latency constraints
