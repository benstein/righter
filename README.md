# Righter - Elite Writing & Editing System

Multi-agent Claude Code configuration for transforming draft documents into exceptional, polished content.

## What It Does

Coordinates multiple specialist AI agents to rigorously refine written content:
- **Tone Consistency** - Ensures consistent voice and appropriate register
- **Authenticity** - Eliminates AI tells and bland corporate speak
- **Clarity** - Ensures clear, precise communication
- **Structure** - Evaluates flow, pacing, and organization

## Quick Start

```bash
cd /Users/ben/Work/righter
claude
/refine your-draft.md
```

Or just paste content and ask for improvement.

## How It Works

1. Orchestrator asks context questions (purpose, audience, tone)
2. Applies 4 specialist review perspectives to each section
3. Creates improved version
4. Iterates multiple rounds until excellent
5. Delivers polished markdown ready for Google Docs

## Configuration

Located in `.claude/`:
- `agents/` - 5 specialized agents (orchestrator uses Sonnet 4.5)
- `commands/` - `/refine` command
- `skills/` - Document processor

## Usage

See [HOW_TO_USE.md](HOW_TO_USE.md) for complete guide.

## Features

- Hyper-critical iterative refinement (not just one pass)
- Hunts for 20+ AI tells ("delve into", "leverage", "robust", etc.)
- Multiple revision rounds per section
- Context-aware editing based on your goals
- Preserves formatting for Google Docs compatibility

## Model Configuration

All agents use Sonnet 4.5 for optimal speed/quality balance. Can be changed by editing `model:` field in `.claude/agents/*.md`.
