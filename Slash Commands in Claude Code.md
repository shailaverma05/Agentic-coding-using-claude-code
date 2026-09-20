# Slash Commands & Session Management in Claude Code

## Overview
An in-depth reference on how Claude Code uses slash commands (`/...`) to convert repetitive developer workflows into instant triggers, manage conversation lifecycles/sessions, balance model selection, enforce security permissions, and inspect token consumption.

---

## 1. What Are Slash Commands?
* **Definition:** Predefined shortcuts starting with a `/` typed directly into a Claude Code session that trigger immediate, deterministic actions or workflows without writing long natural-language prompts.
* **Two Core Types:**
  * **Built-in Commands:** Out-of-the-box tools provided by Anthropic (e.g., `/model`, `/permissions`, `/exit`).
  * **Custom Commands:** User-defined, project-specific macros configured to automate recurring engineering routines.

---

## 2. Session Lifecycle & Hygiene
A **session** is a single conversational instance with Claude Code that tracks execution history, tool calls, and LLM responses.

* **Lifecycle Commands:**
  * Launch/Start: `claude`
  * Terminate Session: `/exit`
  * Resume Previous Sessions: `claude -r` from the terminal (or `/resume` inside an active session).
  * Rename Active Session: `/rename <session-name>` (replaces automatic LLM title generation for easy tracking).
  * Session Context Export: `/export <filename.md>` (dumps the complete chat/tool history into a Markdown file for future architecture or refactoring context).
* **Engineering Best Practices:**
  * **One Feature Per Session:** Keep sessions focused on a single feature or bug to avoid token bloat and context contamination.
  * **Frequent Commits:** Make git commits at clear milestones inside the session before starting the next chunk of work.
  * **Context-Free Inquiries (`/btw`):** Ask side-track or theoretical questions (e.g., framework lookups) without polluting the main model context window.

---

## 3. Frontier Model Strategy (`/model`)
Claude Code allows hot-swapping models depending on the engineering task:

* **Claude 3.7 / Opus:** 
  * High reasoning capability, expensive token cost.
  * **Best For:** Architecture planning, feature specification, database design, and complex problem breakdown.
* **Claude Sonnet (Default):** 
  * Well-balanced speed, coding quality, and token efficiency.
  * **Best For:** Core code generation, test writing, and day-to-day implementation.
* **Claude Haiku:** 
  * Fastest latency and lowest cost.
  * **Best For:** Simple scripting, repetitive formatting, and lightweight queries.
* **Recommended Workflow Pattern:** Plan architectures with Opus -> Implement code with Sonnet.

---

## 4. Quotas, Cost & Developer Diagnostics
* `/usage`: Inspects active token percentages across current session limits and rolling weekly allowances.
* `/extra-usage`: Direct account top-up/recharge interface when hard API quota thresholds are reached.
* `/stats`: Aggregated summary of active coding days, session streaks, and total token usage.
* `/insights`: Generates an interactive local HTML report analyzing interaction efficiency, prompt habits, and recommended workflow improvements.

---

## 5. Security & Permission Management (`/permissions`)
Controls autonomous agent capabilities (file read/write, bash execution, web search).

* **Permission Levels:**
  * `Allow`: Autonomous execution without prompting the user.
  * `Ask`: Prompts user confirmation before each invocation.
  * `Deny`: Hard block; prevents the agent from invoking the tool.
* **Storage Scopes:**
  * `Local Project`: Saved to `.claude/settings.local.json` (machine-specific).
  * `Global Project`: Saved for the whole repository (committed to Git for collaborators).
  * `User Setting`: Applied across all projects on the local machine.

---

## 6. Utilities & Interaction
* `/config`: Interactive UI to toggle extended thinking/reasoning modes, verbosity, and terminal progress indicators.
* `/theme`: Switch terminal UI styling (Dark/Light themes).
* `/voice`: Enables push-to-talk speech input (hold spacebar to speak prompts).
* `/login` & `/logout`: Seamless switching between individual Anthropic subscriber accounts and team API console credentials.

---

## Standalone Mindmap

```mermaid
mindmap
  root((Slash Commands & Sessions))
    Session Lifecycle
      Start & Stop (claude / /exit)
      Resume Flag (claude -r / /resume)
      Session Organization
        /rename for feature tracking
        One task per session rule
        /export to markdown context
      /btw Reference Query
        Side questions without context pollution
    Model Management (/model)
      Opus
        High reasoning & planning
        Architectural spec writing
      Sonnet (Default)
        Standard implementation & tests
        Optimal speed & cost ratio
      Haiku
        Lightweight script routines
    Security & Permissions (/permissions)
      Agent Tool Control
        File Read and Write
        Bash Command Execution
        Web Docs Search
      Access Levels
        Allow / Ask / Deny
      Config Scope
        Local Project (.claude/)
        Global Shared Project
        Global Machine User
    Usage & Diagnostics
      /usage (Session & weekly quotas)
      /extra-usage (Direct API top-up)
      /stats (Activity & token metrics)
      /insights (HTML optimization report)
    UI & Interface Config
      /config (Thinking mode toggle)
      /voice (Push-to-talk input)
      /theme (Dark & Light modes)
      /login & /logout (Account switching)
