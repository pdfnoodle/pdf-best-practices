# Page Breaks

> Control where and how content breaks across pages to prevent awkward splits.

## Core Concepts

PDFs have fixed page boundaries. Unlike web pages that scroll infinitely, PDF content must be intelligently divided across pages. Poor page break handling results in:

- Headings orphaned at page bottoms
- Tables split mid-row
- Images separated from captions
- Single lines stranded on new pages

## CSS Properties

### Prevent Breaks Inside Elements

```css
.no-break {
  page-break-inside: avoid;
  break-inside: avoid;
}
```

Use on:
- Cards and boxes
- Table rows with important data
- Image + caption combinations
- List items with multiple lines
- Any logical content block

### Force Breaks

```css
/* Force break before an element */
.page-break-before {
  page-break-before: always;
  break-before: page;
}

/* Force break after an element */
.page-break-after {
  page-break-after: always;
  break-after: page;
}
```

### Keep Elements Together

```css
/* Keep heading with following content */
h1, h2, h3, h4, h5, h6 {
  page-break-after: avoid;
  break-after: avoid;
}
```

### Orphan and Widow Control

```css
p {
  orphans: 3;  /* Minimum lines at bottom of page */
  widows: 3;   /* Minimum lines at top of page */
}
```

## Common Patterns

### Sections and Cards

```css
.section, .card, .box, .panel {
  page-break-inside: avoid;
  break-inside: avoid;
  margin-bottom: 20px;
}
```

### Figures with Captions

```css
figure {
  page-break-inside: avoid;
  break-inside: avoid;
}

figcaption {
  margin-top: 8px;
  font-size: 10pt;
  color: #666;
}
```

```html
<figure>
  <img src="chart.png" width="400" height="300" alt="Sales Chart">
  <figcaption>Figure 1: Q4 Sales Performance</figcaption>
</figure>
```

### Chapter/Section Starts

```css
.chapter, .new-section {
  page-break-before: always;
  break-before: page;
}
```

### Table Rows

```css
tr {
  page-break-inside: avoid;
  break-inside: avoid;
}
```

## Complete Example

```css
/* Page break control system */

/* Never break inside these */
.card,
.box,
.panel,
.section-block,
figure,
tr {
  page-break-inside: avoid;
  break-inside: avoid;
}

/* Keep headings with content */
h1, h2, h3, h4, h5, h6 {
  page-break-after: avoid;
  break-after: avoid;
}

/* Orphan/widow control */
p, li {
  orphans: 3;
  widows: 3;
}

/* Force new page for major sections */
.chapter-start {
  page-break-before: always;
  break-before: page;
}

/* Utility classes */
.no-break {
  page-break-inside: avoid;
  break-inside: avoid;
}

.page-break {
  page-break-before: always;
  break-before: page;
}
```

## Troubleshooting

| Problem | Solution |
| ------- | -------- |
| Heading alone at page bottom | Add `page-break-after: avoid` to headings |
| Content block split awkwardly | Add `page-break-inside: avoid` to container |
| Single line on new page | Increase `orphans` and `widows` values |
| Want section on new page | Add `page-break-before: always` |
| Too much empty space | Reduce margins or allow more breaks |
