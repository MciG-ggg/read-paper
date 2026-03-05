# Paper Summarization Guide

This guide covers how to generate high-quality paper summaries.

## Output Location

Save summary to:
```
~/knowledge/summary_{tag}.md
```

**Important**: Use local project directory (`~/knowledge/`), not `~/.cache/`, and not `~/Documents/knowledge`, pls notice that the `~` is the home directory.

## Tag Selection

Choose a descriptive tag that:
- Relates to the paper's main topic
- Is unique (avoid overwriting existing files)
- Uses snake_case (e.g., `conditional_memory`, `transformer_attention`)

### Tag Examples

| Paper Topic | Suggested Tag |
|-------------|---------------|
| Language model scaling | `llm_scaling_laws` |
| Attention mechanism | `efficient_attention` |
| Memory mechanism | `context_compression` |

## Summary Structure

### Recommended Format

```markdown
# {Paper Title}

**arXiv ID**: {id}
**Authors**: {authors}
**Date**: {publication_date}

## Abstract

{Brief summary of the paper's main contribution}

## Key Findings

- Finding 1
- Finding 2
- Finding 3

## Technical Details

### Method

{Description of the proposed method}

### Results

{Key experimental results}

## Relevance to Project

{Connection to current project context}

## Potential Applications

- Application 1
- Application 2

## Questions/Follow-ups

- Question 1
- Question 2
```

## Quality Guidelines

### Do ✅

1. **Be concise**: Focus on key insights
2. **Connect to context**: Relate to current project
3. **Include technical details**: Methodology matters
4. **Highlight novel contributions**: What's new?

### Don't ❌

1. **Don't copy abstract**: Summarize in your own words
2. **Don't skip methodology**: Technical depth is important
3. **Don't ignore limitations**: Note constraints
4. **Don't over-quote**: Paraphrase key points

## Length Guidelines

| Section | Target Length |
|---------|---------------|
| Abstract | 2-3 sentences |
| Key Findings | 3-5 bullet points |
| Technical Details | 1-2 paragraphs |
| Relevance | 1 paragraph |

## Connection to Project

When relating to the current project:

1. **Identify overlaps**: What problems does this solve?
2. **Note potential applications**: How can we use this?
3. **Consider implementation**: What's needed to apply?
4. **Highlight risks**: Any concerns or limitations?

## Review Checklist

Before finalizing:

- [ ] Title and metadata correct?
- [ ] Key findings captured?
- [ ] Methodology explained?
- [ ] Project connection clear?
- [ ] Tag is unique?
- [ ] File saved to correct location?
