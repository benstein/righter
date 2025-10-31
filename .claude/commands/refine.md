---
description: Refine and improve a draft document through multi-agent iterative editing
---

# Document Refinement Command

You are starting a document refinement session. Your goal is to transform draft content into exceptional, publication-ready writing.

## Your Task

1. **Invoke the writing-orchestrator agent** to handle this refinement
2. Pass along any specific user instructions or preferences
3. The orchestrator will handle the multi-agent editing workflow

## What the Orchestrator Will Do

The writing-orchestrator agent will:
- Gather context about purpose, audience, and tone
- Analyze the document structure and content
- Coordinate multiple specialist editing agents
- Iterate through multiple revision rounds
- Check in with the user for feedback
- Deliver polished, publication-ready content

## Specialist Agents Involved

The orchestrator coordinates these specialist agents:

1. **Tone Consistency Editor**: Ensures consistent voice and appropriate register throughout
2. **Authenticity Editor**: Eliminates AI tells, bland language, and generic corporate speak
3. **Clarity Editor**: Ensures ideas are communicated clearly and precisely
4. **Structure Editor**: Evaluates flow, pacing, and organization

## Your Role

Your job is simple:
1. Use the Task tool to invoke the "writing-orchestrator" agent
2. Provide the document content, file path, OR Google Docs URL
3. Pass along any user instructions (e.g., "make this clearer", "more professional tone")
4. Let the orchestrator handle the rest

## Input Types Supported

The orchestrator can work with:

1. **Google Docs URL**: `https://docs.google.com/document/d/ABC123/edit`
   - Orchestrator will read from Google Docs
   - Create revision tabs in the same document
   - Original stays safe, revisions in new tabs

2. **Local file path**: `/path/to/draft.md`
   - Orchestrator will read the file
   - Output markdown for you to review

3. **Pasted content**: User pastes text directly
   - Orchestrator works with the text
   - Output markdown for you to review

## Example Invocations

**With Google Docs URL:**
```
I'll start the document refinement process by invoking the writing orchestrator agent.

[Use Task tool with subagent_type="general-purpose"]

Prompt: "You are the writing-orchestrator agent. The user wants to refine this Google Doc: https://docs.google.com/document/d/ABC123/edit. User's request: [specific instructions or 'make it way better']. Please follow your defined workflow, read from Google Docs using MCP tools, and create revision tabs."
```

**With local file:**
```
I'll start the document refinement process by invoking the writing orchestrator agent.

[Use Task tool with subagent_type="general-purpose"]

Prompt: "You are the writing-orchestrator agent. The user wants to refine the file at: /path/to/draft.md. User's request: [specific instructions]. Please follow your defined workflow."
```

**With pasted content:**
```
I'll start the document refinement process by invoking the writing orchestrator agent.

[Use Task tool with subagent_type="general-purpose"]

Prompt: "You are the writing-orchestrator agent. The user wants to refine this content: [pasted text]. User's request: [specific instructions]. Please follow your defined workflow."
```

## Important Notes

- The orchestrator has full instructions on the editing workflow
- It will coordinate all specialist agents automatically
- It will check in with the user when needed
- Trust the process - it's designed for rigorous iteration

Now proceed to invoke the writing-orchestrator agent with the user's document and any specific instructions.
