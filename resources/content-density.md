# Content Density

> Optimize content distribution to avoid sparse pages and professional-looking layouts.

## The Problem

A page with only 10-20% content looks unprofessional. Common causes:
- Excessive margins or padding
- Large fixed spacing between sections
- Content blocks that don't fill pages efficiently
- Poor page break decisions

## Strategies

### 1. Estimate Content Height

Before structuring the document, estimate how much content you have:

| Content Type | Approximate Height |
| ------------ | ------------------ |
| Heading (h1) | 40-50px |
| Heading (h2) | 30-40px |
| Paragraph | ~20px per line |
| Table row | 35-45px |
| Image | Explicit height + caption |

**A4 safe content height:** ~1043px per page (with 40px margins)

### 2. Use Flexible Spacing

```css
/* Use moderate, consistent spacing */
section {
  margin-bottom: 24px;
}

h1 { margin: 0 0 16px 0; }
h2 { margin: 24px 0 12px 0; }
h3 { margin: 20px 0 10px 0; }

p {
  margin: 0 0 12px 0;
}
```

### 3. Compact Variants

Create tighter spacing for dense content:

```css
/* Compact spacing for data-heavy sections */
.compact h2 { margin: 16px 0 8px 0; }
.compact h3 { margin: 12px 0 6px 0; }
.compact p { margin: 0 0 8px 0; }
.compact table { margin: 8px 0; }
```

### 4. Group Related Content

Keep related items together so they flow naturally:

```css
.content-group {
  page-break-inside: avoid;
  break-inside: avoid;
}
```

## Reflow Strategies

If the last page has minimal content, try these adjustments:

### Reduce Margins

```json
{
  "margin": {
    "top": "35px",
    "right": "35px",
    "bottom": "35px",
    "left": "35px"
  }
}
```

### Tighten Line Height

```css
body {
  line-height: 1.4;  /* Instead of 1.5 */
}
```

### Reduce Section Spacing

```css
section {
  margin-bottom: 16px;  /* Instead of 24px */
}
```

### Smaller Font for Dense Data

```css
table {
  font-size: 10pt;  /* Instead of 11pt */
}

.dense-text {
  font-size: 11pt;  /* Instead of 12pt */
}
```

**Minimum readable sizes:**
- Body text: 11pt
- Table data: 10pt
- Captions/footnotes: 9pt

## Content-Aware Layout

### Single Page Documents

For content that should fit one page (invoices, certificates):

```css
.single-page {
  max-height: 1043px;  /* A4 minus margins */
  overflow: hidden;
}
```

### Dynamic Spacing

Use flexbox to distribute space evenly:

```css
.page-content {
  display: flex;
  flex-direction: column;
  min-height: 1043px;
}

.page-content .spacer {
  flex-grow: 1;
}
```

### Conditional Density

Apply density classes based on content amount:

```html
<!-- For lots of content -->
<body class="dense">

<!-- For minimal content -->
<body class="spacious">
```

```css
.dense {
  font-size: 11pt;
  line-height: 1.4;
}

.dense section { margin-bottom: 16px; }

.spacious {
  font-size: 12pt;
  line-height: 1.6;
}

.spacious section { margin-bottom: 32px; }
```

## Common Patterns

### Reports with Variable Content

```css
/* Flexible section spacing */
.report-section {
  margin-bottom: 20px;
  page-break-inside: avoid;
}

.report-section:last-child {
  margin-bottom: 0;
}

/* Tighten if many sections */
.report.dense .report-section {
  margin-bottom: 12px;
}
```

### Invoice Line Items

```css
/* Compact table for many items */
.invoice-items.many-rows td {
  padding: 4px 8px;
  font-size: 10pt;
}

/* Normal spacing for few items */
.invoice-items td {
  padding: 8px 12px;
  font-size: 11pt;
}
```

## Checklist

Before generating the PDF:

- [ ] Estimate total content height
- [ ] Check if last page has < 25% content
- [ ] If sparse, consider: reducing margins, tightening spacing, or smaller fonts
- [ ] Group related content to prevent awkward breaks
- [ ] For single-page docs, verify content fits
