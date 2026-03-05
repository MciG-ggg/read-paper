# PDF Paper Processing Guide

This guide details how to process PDF papers using the pdf skill.

## Overview

For PDF files, use the `pdf` skill to extract content. This is preferred for:
- Scanned documents (OCR required)
- Papers without TeX source
- Quick content extraction

## Processing Steps

### Step 1: Invoke PDF Skill

```
Skill: pdf
```

This loads the pdf skill which provides:
- pypdf for basic operations
- pdfplumber for text/table extraction
- reportlab for PDF creation

### Step 2: Extract Text

Use pdfplumber for best text extraction:

```python
import pdfplumber

with pdfplumber.open(pdf_path) as pdf:
    text = ""
    for page in pdf.pages:
        text += page.extract_text() or ""
```

### Step 3: Extract Tables (if needed)

```python
with pdfplumber.open(pdf_path) as pdf:
    for i, page in enumerate(pdf.pages):
        tables = page.extract_tables()
        # Process tables
```

### Step 4: Handle Scanned PDFs

If text extraction returns empty results, use OCR:

```python
from pdf2image import convert_from_path
import pytesseract

images = convert_from_path(pdf_path)
text = ""
for image in images:
    text += pytesseract.image_to_string(image)
```

### Step 5: Analyze Content

After extraction, analyze:
- Title (usually first line or from metadata)
- Abstract (often on first page)
- Section headings
- Figures and tables
- References

## PDF Metadata

Extract metadata for paper identification:

```python
from pypdf import PdfReader

reader = PdfReader(pdf_path)
metadata = reader.metadata
# title, author, subject, creator
```

## Output Organization

Structure extracted content:
```
{project}/knowledge/{paper_id}/
├── text.txt          # Full text
├── tables.md         # Extracted tables
├── metadata.json     # Title, author, etc.
└── summary_{tag}.md  # Final summary
```

## Best Practices

1. **Check if searchable**: Try text extraction first
2. **Use OCR only if needed**: It's slower
3. **Preserve layout**: Use `-layout` flag with pdftotext
4. **Extract images**: Use pdfimages for figures

## Integration with arXiv Workflow

If PDF is available from arXiv:
1. Try arXiv TeX source first (better quality)
2. Fall back to PDF if source unavailable
3. Use consistent output format
