# 😎 Awesome-RAG Agent Plugin

An [Agent Plugin](https://code.visualstudio.com/docs/agent-customization/agent-plugins) built from [Awesome-RAG](https://github.com/Danielskry/Awesome-RAG). It gives coding agents RAG architecture, evaluation, and production guidance directly in the editor.

Works in VS Code, GitHub Copilot CLI, and Claude Code. The plugin format is shared across all three.

## Skills

- [`rag-advisor`](skills/rag-advisor/SKILL.md): pick a RAG architecture pattern and framework
- [`rag-evaluator`](skills/rag-evaluator/SKILL.md): design an evaluation plan, diagnose retrieval/grounding failures
- [`rag-production-review`](skills/rag-production-review/SKILL.md): audit a pipeline before shipping

## Agent

- [`RAG Architect`](agents/rag-architect.agent.md): a dedicated agent for RAG design and review conversations, using the skills above as reference material

## Install

1. Open Settings and search `chat.plugins.marketplaces`.
2. Add `https://github.com/Danielskry/Awesome-RAG-Agent-Plugin`.
3. Reload the window.
4. Open the Extensions view and search `@agentPlugins awesome-rag`.
5. Click Install.

## Usage

Invoke a skill directly (`/rag-advisor`, `/rag-evaluator`, `/rag-production-review`) or ask naturally. The right skill loads automatically. Switch to the **RAG Architect** agent for a session focused on RAG design.
