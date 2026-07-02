# 😎 Awesome-RAG Agent Plugin

An [Agent Plugin](https://code.visualstudio.com/docs/agent-customization/agent-plugins) built from [Awesome-RAG](https://github.com/Danielskry/Awesome-RAG). It gives coding agents RAG architecture, evaluation, and production guidance directly in the editor.

Works in VS Code, GitHub Copilot CLI, and Claude Code. The plugin format is shared across all three.

## What it includes

### Skills

- [`rag-advisor`](skills/rag-advisor/SKILL.md): choose a RAG architecture pattern and framework
- [`rag-evaluator`](skills/rag-evaluator/SKILL.md): design evaluation plans and diagnose retrieval or grounding failures
- [`rag-production-review`](skills/rag-production-review/SKILL.md): review a RAG pipeline before production

### Agent

- [`RAG Architect`](agents/rag-architect.agent.md): a focused agent for RAG design, review, and evaluation conversations

## Use it for

- Choosing between naive RAG, advanced RAG, agentic RAG, GraphRAG, multimodal RAG, and other patterns
- Reviewing a RAG implementation
- Designing a RAG evaluation plan
- Finding retrieval, chunking, grounding, or citation issues
- Checking production readiness
- Avoiding unnecessary architecture complexity

## Install

### VS Code

Install directly from source:

1. Open the Command Palette with `Ctrl+Shift+P` or `Cmd+Shift+P` on macOS.
2. Run:

```text
Chat: Install Plugin From Source
```

3. Paste this repository URL:

```text
https://github.com/Danielskry/Awesome-RAG-Agent-Plugin
```

You can also add it as a plugin marketplace in `settings.json`:

```json
{
  "chat.plugins.marketplaces": [
    "Danielskry/Awesome-RAG-Agent-Plugin"
  ]
}
```

Then open the Agent Plugins view in Extensions and search:

```text
@agentPlugins awesome-rag
```

### GitHub Copilot CLI

```bash
copilot plugin marketplace add Danielskry/Awesome-RAG-Agent-Plugin
copilot plugin install awesome-rag@awesome-rag
```

### Claude Code

```text
/plugin marketplace add Danielskry/Awesome-RAG-Agent-Plugin
/plugin install awesome-rag@awesome-rag
/reload-plugins
```
## Usage

Invoke a skill directly (`/rag-advisor`, `/rag-evaluator`, `/rag-production-review`) or ask naturally. The right skill loads automatically. Switch to the **RAG Architect** agent for a session focused on RAG design.
