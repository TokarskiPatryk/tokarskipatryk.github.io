+++
title = "Markdown Showcase Post"
description = "A practical post to verify how Markdown features render in the current Hugo theme."
date = 2026-04-16T00:00:00Z
draft = true
tags = ["markdown", "hugo", "demo"]
categories = ["testing"]
+++

This post is a visual checklist for Markdown rendering. If anything looks off, you can use this page as a reference point.

---

## Headings

### Level 3 heading

#### Level 4 heading

##### Level 5 heading

## Emphasis and inline formatting

- *Italic text*
- **Bold text**
- ***Bold and italic***
- ~~Strikethrough~~
- Inline code: `SELECT * FROM demo_table LIMIT 10;`

## Links

- Internal link: [About](/about/)
- Internal link: [Contact](/contact/)
- External link: [Hugo documentation](https://gohugo.io/documentation/)

## Blockquote

> Good documentation reduces support tickets.
>
> And good examples reduce confusion.

## Lists

### Unordered list

- Data ingestion
- Data transformation
- Data quality checks
- Data publishing

### Ordered list

1. Gather requirements
2. Build a simple version
3. Validate outputs
4. Iterate

### Nested list

- Platforms
  - Snowflake
  - Azure Synapse
  - PostgreSQL
- Languages
  - SQL
  - Python
  - R

### Task list

- [x] Add post front matter
- [x] Add mixed Markdown examples
- [x] Verify rendering in light and dark mode
- [ ] Add any missing style overrides

## Table

| Feature | Example | Status |
| --- | --- | --- |
| Bold text | `**bold**` | Tested |
| Code block | fenced code block | Tested |
| Footnote | `[^1]` | Tested |

## Code blocks

```bash
hugo server -D
```

```python
def validate_row_count(current_count: int, previous_count: int) -> bool:
    return current_count >= previous_count


print(validate_row_count(1024, 1000))
```

```json
{
  "pipeline": "daily_reporting",
  "source": "raw_events",
  "target": "analytics_mart",
  "refresh_minutes": 15
}
```

## Image

![Profile image test](/images/avatar.jpg "Avatar rendering test")

## Notice shortcode

{{< notice tip "Tip" >}}
Use this page after each style change to quickly confirm if Markdown blocks still render as expected.
{{< /notice >}}

{{< notice warning "Warning" >}}
If list markers disappear again, check custom CSS overrides and theme updates first.
{{< /notice >}}

## Mermaid shortcode

{{< mermaid >}}
flowchart TD
    A[Raw Data] --> B[Staging]
    B --> C[Transformations]
    C --> D[Data Quality]
    D --> E[Reporting]
{{< /mermaid >}}

## Footnotes

This is a sentence with a footnote.[^1]

[^1]: Footnotes are useful for comments that should not interrupt the main narrative.
