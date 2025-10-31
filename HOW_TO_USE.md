# Elite Writer & Editor - Quick Guide

## Installation Complete! ✅

The multi-agent writing system is now installed **locally in this directory only**.

## Location

```
/Users/ben/Work/righter/.claude/
├── agents/              # 5 specialized editing agents
├── commands/            # /refine command
└── skills/              # document-processor skill
```

## How to Use

### Step 1: Start Claude in This Directory

```bash
cd /Users/ben/Work/righter
claude
```

**Important**: The agents are ONLY available when you start Claude from this directory (or subdirectories).

### Step 2: Verify It's Loaded

```bash
/agents
```

You should see:
- writing-orchestrator
- tone-consistency-editor
- authenticity-editor
- clarity-editor
- structure-editor

### Step 3: Use It!

#### Option A: With Google Docs URL (Recommended!)

```bash
/refine https://docs.google.com/document/d/YOUR_DOC_ID/edit
```

The orchestrator will:
1. Read your document from Google Docs
2. Ask context questions
3. Create revision tabs (Revision 1, Revision 2, etc.)
4. Your original stays safe in the first tab
5. Review revisions side-by-side in Google Docs

**Setup required:** See [GOOGLE_OAUTH_SETUP.md](GOOGLE_OAUTH_SETUP.md) for one-time OAuth configuration (5 minutes).

#### Option B: With local file

```bash
/refine path/to/your-draft.md
```

Outputs markdown you can copy.

#### Option C: Paste content from Google Docs

1. Copy text from your Google Doc
2. Paste into Claude Code
3. Use `/refine` or just say "refine this"
4. Orchestrator creates improved version
5. Copy improved markdown back to Google Docs

#### Option D: Just ask for help

```
I have a draft blog post that needs improvement. Can you help make it clearer and more engaging?
```

The orchestrator will automatically activate and start asking you questions.

#### Option D: Paste content directly

```
Please refine this draft:

[paste your content here]
```

Outputs markdown you can copy.

## What Happens

1. **Orchestrator asks context questions**:
   - What's the purpose?
   - Who's the audience?
   - What tone is appropriate?
   - Any constraints?

2. **Multi-agent review** (for each section):
   - Tone Consistency Editor reviews voice
   - Authenticity Editor hunts AI tells
   - Clarity Editor checks comprehension
   - Structure Editor evaluates flow

3. **Iterative refinement**:
   - Creates improved version
   - All agents re-review
   - Continues until excellent
   - Checks in with you

4. **Delivers polished markdown**:
   - Ready to paste into Google Docs
   - Formatting preserved
   - All AI tells eliminated

## Test Document

Try it with the included test document (has 20+ AI tells):

```bash
cd /Users/ben/Work/righter
claude /refine .claude-plugin-writer-editor/test-draft.md
```

## Files You Can Work With

The system works with:
- Markdown files (`.md`)
- Text files (`.txt`)
- Pasted content from Google Docs
- Any text content

## Output Format

You'll get clean markdown that you can:
- Paste directly into Google Docs
- Save as a file
- Copy to clipboard
- Use in any markdown editor

## Scope

**These agents are ONLY active in `/Users/ben/Work/righter`**

When you work in other directories, they won't interfere with your coding or other work.

## Example Session

```
You: cd /Users/ben/Work/righter
You: claude
You: I need to refine this blog post draft: [paste content]

Claude: I'll use the writing-orchestrator to help refine your blog post.

Orchestrator: I'll help transform your draft into polished content.
First, let me understand the context:

1. What is the primary purpose of this blog post?
   (educate, persuade, entertain, inform, etc.)

2. Who is your target audience?
   (technical level, role, background, etc.)

[... you answer questions ...]

Orchestrator: Perfect. Analyzing your draft...

I've identified several areas for improvement:
- Multiple AI tells ("delve into", "leverage", "robust")
- Some tone inconsistencies
- Clarity could be improved in sections 2-3
- Structure flows well overall

Working through section by section with all 4 specialist agents...

[Processing with updates]

Orchestrator: Here's your refined blog post:

[Beautiful polished output]

Changes made:
- Eliminated 12 AI tells and generic phrases
- Made tone consistently conversational for developers
- Improved technical explanations with concrete examples
- Enhanced flow between sections
```

## Quick Reference

**Start**: `cd /Users/ben/Work/righter && claude`

**Check agents loaded**: `/agents`

**Refine a file**: `/refine your-draft.md`

**Refine pasted text**: Just paste and ask for improvement

**Test it**: `/refine .claude-plugin-writer-editor/test-draft.md`

## Documentation

Full documentation available in `.claude-plugin-writer-editor/`:
- `README.md` - Complete guide
- `QUICKSTART.md` - 5-minute start
- `ARCHITECTURE.md` - How it works
- `test-draft.md` - Sample document

Enjoy transforming your drafts into exceptional content! 🚀
