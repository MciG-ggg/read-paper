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
Input → Detect Type → Process → Summarize → Output
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

See [summarization.md](references/summarization.md) for summary guidelines.

Output to `./knowledge/summary_{tag}.md` in local project directory.

## Detailed Guides

For detailed processing instructions, see:

| Guide | Content |
|-------|---------|
| [arxiv.md](references/arxiv.md) | arXiv TeX source download, parsing, analysis |
| [pdf.md](references/pdf.md) | PDF text extraction, table extraction |
| [summarization.md](references/summarization.md) | Summary format, tag selection, quality guidelines |

## Key Principles

1. **Cache downloaded content**: Store in `~/.cache/nanochat/knowledge/{paper_id}/`
2. **Use local output directory**: `./knowledge/` not `~/.cache/`
3. **Connect to project context**: Relate paper content to current project
4. **Generate useful tags**: Choose descriptive tags for summarization
