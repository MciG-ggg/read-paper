# Obsidian Output Guide

This guide explains how to generate Obsidian-compatible markdown files with proper tag management.

## Output Location

Directly to your Obsidian vault:
```
~/Documents/obsidian/80-paper/
```

## Tag Management Workflow

### Step 1: Generate Candidate Tags

Based on paper content, generate 2-4 candidate tags:
- Paper main topic (e.g., `llm_scaling`, `transformer_optimization`)
- Methodology type (e.g., `efficient_attention`, `mixture_of_experts`)
- Application domain (e.g., `code_generation`, `multimodal`)

### Step 2: Check Existing Tags (Required)

**Before adding any tag**, search claude-mem to check if similar tags exist:

```python
# Use claude-mem mem-search tool
search(query="{candidate_tag}", limit=10, project="paper-tags")
```

### Step 3: Match or Create Tag

**If similar tag exists**:
- Use the existing tag
- Note the relationship in memory

**If no similar tag found**:
- Create new tag
- Save to claude-mem after adding to document

#### !!!Attention

the tags' structural should follow the architecture below:`Paper/{big tag}/{small tag}/{small small tag} ...`
which the tag in the front represent a bigger concept, and the tag behind represent a concrete concept.

for some examples:
tags
- Paper/rl/multiagent
- Paper/sim2real
- Paper/EmbodiedAI/VLA
- Paper/EmbodiedAI/VLN 

### Step 4: Save New Tag to claude-mem (If Created)

```python
# Use save_memory tool
save_memory(
    text=f"New paper tag: {tag_name} - {description}",
    title=f"Tag: {tag_name}",
    project="paper-tags"
)
```

## Obsidian Format

### Frontmatter

```yaml
---
title: {Paper Title}
date: {YYYY-MM-DD}
tags:
  - {tag1}
  - {tag2}
  - {paper_topic}
aliases:
  - {Paper Title}
  - {arXiv ID}
---

### Metadata Block

```markdown
> [!info]- Metadata
> - **arXiv**: [ID](url)
> - **Authors**: Author 1, Author 2
> - **Year**: 2024
> - **Topics**: #tag1 #tag2
```

### Callouts Usage

Use Obsidian callouts for structure:

```markdown
> [!abstract]+ Abstract
> {Summary}

> [!key-findings]- Key Findings
> - Finding 1
> - Finding 2

> [!method]+ Method
> {Methodology description}

> [!results] Results
> {Key results}
```

### Wikilinks

Link to related concepts:

```markdown
Related: [[topic1]], [[topic2]], [[methodology]]
```

## Complete Example

```markdown
---
title: Scalable监督学习 for Language Models
date: 2024-03-15
tags:
  - llm_scaling
  - supervised_learning
  - transformer
aliases:
  - Scalable监督学习 for Language Models
  - arXiv:2403.XXXXX
---

# Scalable监督学习 for Language Models

> [!info]- Metadata
> - **arXiv**: [2403.XXXXX](https://arxiv.org/abs/2403.XXXXX)
> - **Authors**: Author 1, Author 2
> - **Year**: 2024
> - **Topics**: #llm_scaling #supervised_learning

## Abstract

> [!abstract]+
> Paper summary here...

## Key Findings

> [!key-findings]-
> - Finding 1
> - Finding 2

## Method

> [!method]+
> Description of methodology...

## Results

> [!results]
> Key experimental results...

## Related

Related: [[llm_scaling_laws]], [[transformer_architecture]]
```

## Integration with obsidian-markdown Skill

For advanced formatting, use the `obsidian:obsidian-markdown` skill:

```
Skill: obsidian-markdown
```

This provides:
- Proper frontmatter generation
- Wikilink suggestions
- Callout formatting
- Property syntax

## Tag Storage Structure (claude-mem)

```json
{
  "tag": "llm_scaling",
  "description": "Language model scaling laws and efficient training",
  "related_tags": ["transformer", "efficient_training"],
  "paper_count": 5,
  "created_date": "2024-03-15"
}
```

## Quality Checklist

- [ ] Frontmatter has title, date, tags, aliases?
- [ ] Tags checked against claude-mem first?
- [ ] New tags saved to claude-mem?
- [ ] Callouts used for structured content?
- [ ] Wikilinks to related topics included?
- [ ] File saved to correct location?
