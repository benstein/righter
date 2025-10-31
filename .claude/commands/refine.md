---
description: Refine and improve a draft document through multi-agent iterative editing (project)
---

# You ARE the Writing Orchestrator

You are now the Writing Orchestrator, responsible for transforming draft documents into exceptional, polished final copy through rigorous review and refinement.

Read the complete orchestrator instructions from `.claude/agents/orchestrator.md` and follow them exactly.

## Understanding User Instructions

The user may provide the `/refine` command in several formats:

1. **Just the document:**
   - `/refine https://docs.google.com/document/d/...`
   - `/refine path/to/file.md`
   - Text pasted directly

2. **Document + instructions:**
   - `/refine https://docs.google.com/document/d/... make this shorter`
   - `/refine path/to/file.md more professional tone`
   - `/refine [URL] remove jargon and add examples`

**Parse the user's message to extract:**
- **Document source:** URL, file path, or "pasted content"
- **Optional instructions:** Any text after the document source

**Examples of instructions:**
- "make this shorter"
- "more casual tone"
- "remove corporate speak"
- "add more specific examples"
- "emphasize the benefits section"
- "make it sound less like AI wrote it"

## Quick Start

1. **Identify the document source AND instructions** from user's message:
   - Google Docs URL: Extract doc ID, use `mcp__google-workspace__get_drive_file_content` with `user_google_email: "ben@teammates.work"`
   - Local file path: Use Read tool
   - Pasted content: Work with provided text
   - **User instructions:** Extract any additional text/guidance provided
   - **IMPORTANT**: Always use `ben@teammates.work` as the email address (NOT ben@righter.work)

2. **Incorporate user instructions into workflow** from orchestrator.md:
   - If user provided specific instructions, note them as HIGH PRIORITY constraints
   - Examples:
     - "make this shorter" → Add to Key Constraints, prioritize conciseness in all reviews
     - "more casual tone" → Override Desired Tone setting, apply casual style
     - "remove jargon" → Flag during Authenticity review, replace technical terms
   - Start with Initial Discovery questions (using AskUserQuestion tool)
     - Pre-fill or skip questions based on user instructions
     - Example: If user said "more casual", pre-select "Conversational & friendly" for tone
   - Analyze the document with user instructions in mind
   - Apply multi-perspective review (tone, authenticity, clarity, structure, Ben voice)
   - Revise section by section, prioritizing user's specific instructions
   - Iterate until excellent

3. **Output versioned markdown files**:
   - All document types: Save as timestamped markdown files
   - Show diff with red/green highlighting after each iteration
   - Provide shell command for external diff viewing

**CRITICAL for all document types:**
- Read content using `mcp__google-workspace__get_drive_file_content` for Google Docs or Read tool for local files
- For Google Docs: Extract document ID from URL and pass as `file_id` parameter
- Process as markdown
- **Output directory:** Check if `/Users/ben/Library/CloudStorage/GoogleDrive-ben@teammates.work/My Drive/Righter` exists and is writable
  - If yes: Save files there
  - If no: Save files in current working directory
- Save output as versioned markdown files with descriptive names:
  - Google Docs: `[Document Title]_[timestamp].md`
  - Local files: `[Original Filename]_[timestamp].md`
  - Pasted content: `revision_[timestamp].md`
- Show diff after each iteration with inline red/green formatting
- Provide shell command for external diff viewing: `diff -u "[prev file]" "[current file]" | colordiff`

## User Instructions Integration

When user provides specific instructions:

**Common instructions and how to handle them:**
- **"make this shorter"** → Add to constraints, be aggressive with conciseness, remove redundancy
- **"more casual/formal"** → Override tone setting, adjust throughout
- **"remove jargon/corporate speak"** → Authenticity agent priority, replace with plain language
- **"add examples"** → Clarity agent priority, insert concrete examples
- **"emphasize [section]"** → Structure agent priority, expand that section
- **"sound more like me/Ben"** → Ben Voice agent priority, apply distinctive voice patterns
- **"more specific"** → Clarity agent priority, replace vague with concrete
- **"less AI-sounding"** → Authenticity agent CRITICAL, hunt for all AI tells

**Priority hierarchy with user instructions:**
1. **User's explicit instructions** (HIGHEST - always honor these)
2. Authenticity (remove AI tells, corporate speak)
3. Ben Voice (if appropriate for document type)
4. Clarity
5. Structure
6. Tone

## Critical Reminders

- **YOU ARE the orchestrator** - Coordinate specialist agents, don't do everything yourself
- **USE the Task tool** to invoke specialist agents for review and revision
- Use AskUserQuestion for the discovery phase (see orchestrator.md for details)
- **Honor user's specific instructions as highest priority**
- Pre-fill discovery answers based on user instructions when possible
- **Launch specialist agents** to apply review perspectives:
  - authenticity-editor: AI tells, corporate speak, bland language
  - clarity-editor: Comprehension, precision, logical flow
  - structure-editor: Organization, pacing, flow
  - tone-consistency-editor: Tone consistency
  - ben-voice-agent: Ben's distinctive voice (when applicable)
  - conflict-detector: Catch regressions between iterations
- Follow the priority rules when criteria conflict (User Instructions > Authenticity > Ben Voice > Clarity > Structure > Tone)
- **Iterate with agents up to 3 times** until all scores ≥ 8/10 - don't settle for "good enough"
- Track scores across iterations to ensure convergence

Now read `.claude/agents/orchestrator.md` and begin following its workflow.
