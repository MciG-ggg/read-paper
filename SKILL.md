---
name: read-paper
description: "Read and analyze academic papers from arXiv or PDF files. Use when: (1) User provides an arXiv URL (e.g., https://www.arxiv.org/abs/2601.07372), (2) User provides a local PDF file path, (3) User wants to understand paper content and generate summary, (4) User asks to read research paper"
---

# Read Paper - Quick Start

This skill reads academic papers (arXiv or PDF) and generates summaries.

## When to Use

Use this skill when:
- User asks to read an arXiv paper from URL
- User provides a PDF file to analyze
- User wants to understand paper content
- User asks for paper summary or key findings
- User mentions terms like "paper", "research", "academic"

## Supported Input Types

| Input Type | Example | Processing |
|------------|---------|------------|
| arXiv URL | `https://www.arxiv.org/abs/2601.07372` | Download TeX source, parse LaTeX |
| PDF Path | `/path/to/paper.pdf` | Extract text/tables using pdf skill |

## Quick Workflow

```
Input → Detect Type → Process → Tag Management → Summarize → Obsidian Output
```

### Tag Management (Required)

Before generating summary, **you must manage tags**:

1. **Generate candidate tags** from paper content (2-4 tags)
2. **Check existing tags** using claude-mem:
   ```
   Use: claude-mem:mem-search
   Query: {candidate_tag}
   Project: paper-tags
   ```
3. **Match or create**:
   - If similar tag exists → use existing
   - If new → create and save to claude-mem after

4. **Save new tags** to claude-mem:
   ```
   Use: claude-mem:save_memory
   Text: "New paper tag: {tag} - {description}"
   Project: paper-tags
   ```

### Step 1: Detect Input Type

- If URL contains `arxiv.org/abs/` → **arXiv paper**
- If path ends with `.pdf` → **PDF file**
- Otherwise → Ask user to clarify

### Step 2: Process Based on Type

**For arXiv papers**: See [arxiv.md](references/arxiv.md)

**For PDF files**: Use `pdf` skill to extract content:
```
Skill: pdf
```
Then follow the text extraction workflow.

### Step 3: Generate Summary


Output to `~/knowledge/summary_{tag}.md` in Obsidian-native format (frontmatter + callouts).

## Detailed Guides

For detailed processing instructions, see:

| Guide | Content |
|-------|---------|
| [arxiv.md](references/arxiv.md) | arXiv TeX source download, parsing, analysis |
| [pdf.md](references/pdf.md) | PDF text extraction, table extraction |
| [summarization.md](references/summarization.md) | Obsidian-native summary format (frontmatter + callouts), tag selection, quality guidelines |
| [obsidian-output.md](references/obsidian-output.md) | Obsidian format, tag management, claude-mem integration |


## Key Principles

1. **Cache downloaded content**: Store in `~/.cache/nanochat/knowledge/{paper_id}/`
2. **Use local output directory**: `~/knowledge/` not `~/.cache/`
3. **Connect to project context**: Relate paper content to current project
4. **Tag management required**: Always check claude-mem before adding tags
5. **Obsidian-native output**: All summaries use Obsidian format (frontmatter + callouts)

