# Document Processor Examples

This file contains examples of how the document processor skill handles various scenarios.

## Example 1: Processing a Markdown File

**Input File** (`draft.md`):
```markdown
# My Blog Post

This is a draft blog post that needs improvement.

## Section 1

We need to delve into the key aspects here. It's important to note that this is a robust solution.

## Section 2

Furthermore, we should leverage cutting-edge technology to create a seamless experience.
```

**Processing Steps:**
1. Read the file using Read tool
2. Validate markdown structure
3. Pass to writing-orchestrator
4. Receive refined content
5. Format output

**Expected Output Structure:**
```markdown
# My Blog Post

[Improved introduction with better clarity and no AI tells]

## Section 1

[Revised content without "delve into", "robust", "important to note"]

## Section 2

[Improved content without "leverage", "cutting-edge", "seamless"]
```

## Example 2: Processing Pasted Google Docs Content

**User Action:**
User copies content from Google Docs and pastes into Claude Code.

**Input:**
```
Project Update - Q4 2024

Executive Summary
This quarter we've made significant progress on our key initiatives...

Technical Implementation
We leveraged our robust infrastructure to deliver cutting-edge solutions...
```

**Processing:**
1. Receive pasted text
2. Convert to clean markdown with proper heading syntax
3. Identify structure (# for h1, ## for h2, etc.)
4. Pass to orchestrator
5. Receive refined version
6. Format for Google Docs compatibility

**Output:**
```markdown
# Project Update - Q4 2024

## Executive Summary

[Improved version without generic corporate speak]

## Technical Implementation

[Improved version without "leveraged", "robust", "cutting-edge"]
```

## Example 3: Preserving Formatting

**Input with Complex Formatting:**
```markdown
# Technical Guide

## Overview

This guide covers:
- Feature A
- Feature B
- Feature C

### Implementation Steps

1. First step
2. Second step
3. Third step

**Important**: This is a critical note.

> This is a quote from the documentation.

```code
function example() {
  return true;
}
```
```

**Processing Ensures:**
- Heading hierarchy preserved (h1 > h2 > h3)
- Lists maintain structure
- Bold/italic formatting retained
- Block quotes preserved
- Code blocks untouched (content-wise)
- Proper spacing maintained

**Output:**
Same structure, but with improved content quality while preserving all formatting.

## Example 4: Handling Long Documents

**Input:** 5,000-word technical document

**Processing Strategy:**
1. Read entire document
2. Identify major sections
3. Process section by section
4. Maintain context between sections
5. Ensure transitions remain smooth
6. Validate overall document coherence
7. Output complete refined document

**Orchestrator Will:**
- Break down into manageable sections
- Process each with all four specialist agents
- Ensure consistency across sections
- Check overall flow and structure
- Deliver complete refined version

## Example 5: Google Docs URL (with MCP)

**User Input:**
```
"Refine this Google Doc: https://docs.google.com/document/d/1ABC123XYZ/edit"
```

**Processing (with MCP configured):**
1. Use MCP Google Docs tools to read the document
2. Extract content with formatting
3. Convert to markdown
4. Pass through refinement workflow
5. Output markdown that can be:
   - Pasted back into Google Docs
   - Saved as a file
   - Copied directly to clipboard

**Without MCP:**
1. Instruct user to copy-paste content OR export as .docx
2. Process pasted content
3. Deliver refined markdown

## Example 6: Handling Formatting Edge Cases

### Case: Nested Lists

**Input:**
```markdown
- Main item
  - Sub item 1
  - Sub item 2
    - Sub-sub item
- Another main item
```

**Processing:**
- Preserve indentation (2 spaces per level)
- Maintain list structure
- Ensure Google Docs will render correctly

### Case: Mixed Emphasis

**Input:**
```markdown
This has **bold** and *italic* and ***both***.
```

**Output:**
Same emphasis preserved using standard markdown syntax.

### Case: Links

**Input:**
```markdown
Check out [this resource](https://example.com) for more info.
```

**Output:**
Links preserved with standard markdown link syntax.

### Case: Tables (if present)

**Input:**
```markdown
| Column 1 | Column 2 |
|----------|----------|
| Data 1   | Data 2   |
```

**Output:**
Table structure preserved (though Google Docs markdown import has limitations with tables).

## Example 7: Error Handling

### Scenario: File Not Found

**Input:**
```
/refine nonexistent-file.md
```

**Handling:**
1. Attempt to read file
2. Receive error
3. Inform user clearly
4. Ask if they want to paste content instead

### Scenario: Invalid Markdown

**Input:**
```markdown
# Heading

This has some weird formatting issues##

[Broken link](
```

**Handling:**
1. Identify parsing issues
2. Attempt to clean up
3. If unable to parse, inform user
4. Ask for corrected version or manual paste

### Scenario: Empty Document

**Input:**
Empty file or no content

**Handling:**
1. Detect empty content
2. Inform user
3. Ask if this is intentional or if they want to provide content

## Example 8: Output Quality Check

After processing, validate:

```markdown
✓ All headings use proper syntax (#, ##, ###)
✓ Lists are properly formatted (-, 1.)
✓ Emphasis markers are consistent (**bold**, *italic*)
✓ Links are well-formed [text](url)
✓ No stray formatting characters
✓ Proper spacing between elements
✓ No markdown artifacts from conversion
✓ Google Docs compatible
```

## Example 9: Before & After Comparison

**Before:**
```markdown
# Leveraging AI for Enhanced Productivity

In today's digital landscape, it's important to note that organizations
are delving into AI solutions to drive synergy and create robust,
cutting-edge systems that seamlessly integrate with existing workflows.

Furthermore, this paradigm shift enables us to move the needle on key
metrics and leverage low-hanging fruit to boil the ocean on digital
transformation initiatives.
```

**After:**
```markdown
# Using AI to Boost Productivity

Organizations now use AI tools to improve workflows and increase efficiency.
These systems integrate with existing processes to deliver measurable results.

This shift lets companies improve key metrics quickly and make meaningful
progress on digital transformation.
```

**Changes Made:**
- Removed: "Leveraging", "Enhanced" → "Using", "Boost"
- Removed: "In today's digital landscape"
- Removed: "it's important to note"
- Removed: "delving into"
- Removed: "drive synergy"
- Removed: "robust, cutting-edge"
- Removed: "seamlessly integrate"
- Removed: "Furthermore"
- Removed: "paradigm shift"
- Removed: "move the needle"
- Removed: "leverage low-hanging fruit"
- Removed: "boil the ocean"
- Made language more direct and specific
- Improved clarity and authenticity

## Tips for Best Results

1. **Start with structured content**: Having clear sections helps the processor maintain organization

2. **Use standard markdown**: Exotic formatting may not survive the round trip

3. **Keep formatting simple for Google Docs**: Complex tables and layouts have limitations

4. **Provide context**: The more you tell the orchestrator about purpose and audience, the better

5. **Review before final import**: Always check the output before importing to Google Docs

6. **Test the round trip**: Try exporting from Google Docs, processing, and re-importing to verify formatting survives
