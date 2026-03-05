# arXiv Paper Processing Guide

This guide details how to process arXiv papers by downloading and parsing the TeX source.

## Overview

arXiv papers are best read from their LaTeX source, which preserves:
- Mathematical formulas
- Section structure
- Citations and references

## Processing Steps

### Step 1: Normalize the URL

Transform the arXiv abstract URL to source URL:

```
Input:  https://www.arxiv.org/abs/2601.07372
Output: https://www.arxiv.org/src/2601.07372
```

Replace `/abs/` with `/src/`.

### Step 2: Download Source

Download to cache location:
```
~/.cache/nanochat/knowledge/{arxiv_id}.tar.gz
```

If file already exists, skip download.

```bash
# Example download command
curl -L -o ~/.cache/nanochat/knowledge/2601.07372.tar.gz \
  https://www.arxiv.org/src/2601.07372
```

### Step 3: Unpack

Extract to:
```
~/.cache/nanochat/knowledge/{arxiv_id}/
```

```bash
tar -xzf ~/.cache/nanochat/knowledge/2601.07372.tar.gz \
  -C ~/.cache/nanochat/knowledge/
```

### Step 4: Find Entrypoint

Look for main TeX file. Common names:
- `main.tex`
- `paper.tex`
- `{arxiv_id}.tex`

If multiple `.tex` files exist, look for the one that:
- Uses `\documentclass`
- Has `\begin{document}`
- Includes other files via `\input{}` or `\include{}`

### Step 5: Read Paper Content

Read the entrypoint file first, then recursively read:
- `\input{}` files
- `\include{}` files
- Referenced `.bib` files for citations

### Step 6: Analyze Structure

Extract key information:
- Title and authors
- Abstract
- Introduction approach
- Methodology
- Results
- Conclusions

## Cache Management

| Location | Purpose |
|----------|---------|
| `~/.cache/nanochat/knowledge/{id}.tar.gz` | Original download |
| `~/.cache/nanochat/knowledge/{id}/` | Unpacked source |

Check cache before downloading:
```python
import os
cache_path = f"~/.cache/nanochat/knowledge/{arxiv_id}.tar.gz"
if not os.path.exists(os.path.expanduser(cache_path)):
    # Download
```

## Error Handling

### Common Issues

1. **Source not available**: Some papers only have PDF
   - Fall back to PDF processing

2. **Multiple versions**: Use latest version
   - URL pattern: `/src/{id}v{version}`

3. **TeX compilation errors**: Skip non-essential files
   - Focus on reading, not compiling

## Best Practices

1. **Always cache**: Avoid re-downloading
2. **Read in order**: main.tex → includes → bibliography
3. **Extract figures**: Check for `./figures/` or `./img/` directories
4. **Note dependencies**: Track which files include which
