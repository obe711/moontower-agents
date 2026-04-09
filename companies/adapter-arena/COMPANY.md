---
name: Adapter Arena
description: Benchmark company that runs identical coding tasks across all Paperclip agent adapters to compare strengths and weaknesses
slug: adapter-arena
schema: agentcompanies/v1
version: 0.1.0
license: MIT
authors:
  - name: Obe
goals:
  - Run identical coding tasks across all 7 agent adapters
  - Collect structured results with timing and quality metrics
  - Generate a comparative report ranking adapters by capability
---

Adapter Arena is a benchmarking company that evaluates Paperclip's agent adapters head-to-head. A Test Director orchestrates 10 coding challenges, assigning each task to every adapter-specific runner agent. Each runner executes the same task using its configured adapter (Claude Code, Codex, Cursor, Gemini, OpenCode, Pi, OpenClaw). The Test Director collects results and produces a structured comparison report.

## Workflow

1. The Test Director creates tasks from the adapter-benchmark project templates and assigns them to all runner agents
2. Each runner agent independently executes the assigned task using its adapter
3. Runners report results back via task comments with structured output
4. The Test Director collects all results and generates the comparison report using the arena-report skill
5. When new runners are needed, the Test Director assigns a task to the Agent Provisioner specifying the adapter type and configuration. The provisioner creates the new runner agent via the Paperclip hire API.

## Adapters Under Test

| Runner            | Adapter          | Tool                                        |
| ----------------- | ---------------- | ------------------------------------------- |
| claude-runner     | claude_local     | Claude Code CLI                             |
| codex-runner      | codex_local      | OpenAI Codex CLI                            |
| ollama-runner     | claude_ollama    | Claude Code CLI                             |
| cursor-runner     | cursor           | Cursor Agent CLI                            |
| gemini-runner     | gemini_local     | Google Gemini CLI                           |
| opencode-runner   | opencode_local   | OpenCode CLI                                |
| pi-runner         | pi_local         | Pi CLI                                      |
| openclaw-runner      | openclaw_gateway | OpenClaw Gateway                            |
| glm-runner           | claude_ollama    | Claude Code CLI (GLM-5.1:cloud)             |
| kimi-runner          | claude_ollama    | Claude Code CLI (kimi-k2.5:cloud)           |
| minimax-runner       | claude_ollama    | Claude Code CLI (minimax-m2.7:cloud)        |
| qwen3-coder-runner   | claude_ollama    | Claude Code CLI (qwen3-coder-next:cloud)    |
| qwen3dot5-runner     | claude_ollama    | Claude Code CLI (qwen3.5:397b-cloud)        |
| agent-provisioner    | claude_local     | Claude Code CLI (creates new runner agents) |
