---
name: document-processor
description: Skill for processing draft documents from various sources (Google Docs, markdown files, text files) and preparing them for editing workflow
allowed-tools: Read, Write, Grep, Glob
---

# Document Processor Skill

This skill helps you work with draft documents that need editing and refinement.

## When to Use This Skill

Use this skill when:
- User provides a document URL or file path for editing
- Need to extract content from various formats
- Preparing documents for the multi-agent editing workflow
- Converting between formats while preserving structure

## Supported Formats

1. **Markdown files** (.md)
2. **Text files** (.txt)
3. **Google Docs** (via URL or export)
4. **HTML files** (with conversion to markdown)

## Core Functions

### 1. Document Import

When a user provides a document:

1. **Identify the format**
   - Check file extension
   - Validate URLs
   - Determine source type

2. **Extract content**
   - Read the file
   - Preserve formatting (headings, lists, emphasis)
   - Note any issues with extraction

3. **Prepare for editing**
   - Ensure clean markdown format
   - Validate structure
   - Create working copy if needed

### 2. Format Preservation

Maintain these elements during processing:
- Heading hierarchy (h1, h2, h3, etc.)
- Lists (ordered and unordered)
- Emphasis (bold, italic)
- Links
- Block quotes
- Code blocks (if present)

### 3. Output Generation

After editing is complete:

1. **Generate clean markdown**
   - Proper heading syntax
   - Consistent list formatting
   - Clean emphasis markers
   - Well-formed links

2. **Ensure Google Docs compatibility**
   - Use standard markdown syntax
   - Avoid exotic formatting
   - Include proper spacing

3. **Validate output**
   - Check for formatting errors
   - Ensure nothing was lost
   - Confirm readability

## Processing Workflow

```
1. Receive document (file path, URL, or pasted content)
   ↓
2. Extract and validate content
   ↓
3. Convert to clean markdown (if needed)
   ↓
4. Pass to editing orchestrator
   ↓
5. Receive edited content back
   ↓
6. Format for final output
   ↓
7. Deliver markdown ready for Google Docs
```

## Google Docs Integration

### Importing from Google Docs

If user provides a Google Docs URL:
1. Instruct user to export as .docx or copy-paste the content
2. OR use MCP Google Docs integration if configured
3. Convert to markdown while preserving structure

### Exporting to Google Docs

Final output should be markdown that:
- Uses standard heading syntax (`#`, `##`, `###`)
- Uses standard emphasis (`**bold**`, `*italic*`)
- Uses standard lists (`-` or `1.`)
- Includes proper spacing between elements
- Can be copy-pasted directly into Google Docs

### Formatting Guidelines for Google Docs Compatibility

**Headings:**
```markdown
# Heading 1
## Heading 2
### Heading 3
```

**Lists:**
```markdown
- Unordered item
- Another item

1. Ordered item
2. Another item
```

**Emphasis:**
```markdown
**Bold text**
*Italic text*
***Bold and italic***
```

**Links:**
```markdown
[Link text](https://url.com)
```

**Quotes:**
```markdown
> This is a block quote
```

## Common Issues and Solutions

### Issue: Formatting Lost During Copy-Paste
**Solution**: Use plain markdown syntax that Google Docs recognizes natively

### Issue: Nested Lists Not Rendering
**Solution**: Use proper indentation (2 spaces for nesting)

### Issue: Em-dashes Breaking Lines
**Solution**: Convert em-dashes to regular dashes or remove them (per authenticity guidelines)

### Issue: Special Characters Causing Problems
**Solution**: Use HTML entities or standard characters

## Best Practices

1. **Always preserve the original** - Keep a copy before processing
2. **Validate structure** - Check that headings, lists work correctly
3. **Test formatting** - Verify markdown renders correctly
4. **Be conservative** - Don't add exotic formatting
5. **Maintain hierarchy** - Preserve document outline structure

## Integration with Editing Workflow

This skill works hand-in-hand with the editing orchestrator:

1. **Pre-processing**: Clean and prepare document
2. **Handoff**: Pass clean content to orchestrator
3. **Post-processing**: Format edited content for delivery
4. **Validation**: Ensure formatting survived the editing process

## Examples

### Example 1: Processing a Local Markdown File

```markdown
User: "Improve this document: /path/to/draft.md"

1. Read the file
2. Validate markdown syntax
3. Pass to writing-orchestrator agent
4. Receive edited content
5. Format final output
6. Present to user
```

### Example 2: Processing Google Docs Content

```markdown
User: "Here's my draft: [pastes content from Google Docs]"

1. Receive pasted content
2. Convert to clean markdown
3. Preserve formatting elements
4. Pass to writing-orchestrator agent
5. Receive edited content
6. Format for Google Docs re-import
7. Provide markdown output
```

## Quality Checklist

Before passing documents to the orchestrator:
- [ ] Content is in clean markdown format
- [ ] Headings use proper syntax
- [ ] Lists are properly formatted
- [ ] Emphasis markers are consistent
- [ ] No stray formatting artifacts
- [ ] Structure is preserved

After receiving edited content:
- [ ] Formatting is intact
- [ ] Markdown syntax is valid
- [ ] Google Docs compatible
- [ ] All content sections present
- [ ] No formatting errors introduced

Remember: Your job is to handle the technical aspects of document processing so the editing agents can focus on content quality.
