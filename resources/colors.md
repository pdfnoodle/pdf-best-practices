# Colors & Backgrounds

> Ensure colors and backgrounds render correctly in PDF output.

## Critical CSS Property

Always include this in your body styles:

```css
body {
  -webkit-print-color-adjust: exact;
  print-color-adjust: exact;
}
```

**Without this property, background colors may not appear in the generated PDF.**

## PDF Parameters

Always include `printBackground: true`:

```json
{
  "format": "A4",
  "margin": { "top": "40px", "right": "40px", "bottom": "40px", "left": "40px" },
  "printBackground": true
}
```

## Color Guidelines

### Contrast Requirements

Ensure sufficient contrast for readability:

```css
/* Good contrast */
body {
  color: #333;      /* Dark gray text */
  background: #fff; /* White background */
}

/* Minimum for muted text */
.muted {
  color: #666;  /* Don't go lighter than this */
}

/* Links */
a {
  color: #0066cc;  /* Visible blue */
}
```

### Avoid Problematic Colors

| Avoid | Use Instead | Reason |
| ----- | ----------- | ------ |
| `#999` or lighter for text | `#666` or darker | Poor readability |
| Pure black `#000` | `#333` | Softer on eyes |
| Bright saturated colors | Muted versions | Print differently than screen |
| Transparency/opacity | Solid colors | May not render correctly |

## Background Colors

### Solid Backgrounds

```css
/* Table header */
th {
  background-color: #f5f5f5;
}

/* Zebra striping */
tbody tr:nth-child(even) {
  background-color: #fafafa;
}

/* Highlight box */
.highlight {
  background-color: #fff3cd;
  border-left: 4px solid #ffc107;
  padding: 12px;
}

/* Info box */
.info {
  background-color: #e7f3ff;
  border-left: 4px solid #0066cc;
  padding: 12px;
}

/* Success */
.success {
  background-color: #d4edda;
  border-left: 4px solid #28a745;
  padding: 12px;
}

/* Warning */
.warning {
  background-color: #fff3cd;
  border-left: 4px solid #ffc107;
  padding: 12px;
}

/* Error */
.error {
  background-color: #f8d7da;
  border-left: 4px solid #dc3545;
  padding: 12px;
}
```

### Status Badges

```css
.badge {
  display: inline-block;
  padding: 2px 8px;
  border-radius: 4px;
  font-size: 10pt;
  font-weight: 600;
}

.badge-success {
  background-color: #28a745;
  color: #fff;
}

.badge-warning {
  background-color: #ffc107;
  color: #333;
}

.badge-danger {
  background-color: #dc3545;
  color: #fff;
}

.badge-info {
  background-color: #17a2b8;
  color: #fff;
}
```

## Borders

Borders are reliable for visual separation:

```css
/* Section divider */
.divider {
  border-bottom: 1px solid #ddd;
  margin: 20px 0;
}

/* Strong divider */
.divider-strong {
  border-bottom: 2px solid #333;
  margin: 20px 0;
}

/* Card with border */
.card {
  border: 1px solid #ddd;
  border-radius: 4px;
  padding: 16px;
}
```

## Print-Specific Considerations

### Colors May Shift

Screen colors can look different when printed. Test your PDF output and adjust:

```css
/* Screen-only bright color */
@media screen {
  .accent { color: #00bcd4; }
}

/* Darker for print */
@media print {
  .accent { color: #0097a7; }
}
```

### Avoid Gradients

Gradients may not render consistently. Use solid colors:

```css
/* Avoid */
.header {
  background: linear-gradient(to right, #667eea, #764ba2);
}

/* Prefer */
.header {
  background-color: #667eea;
}
```

## Complete Example

```css
body {
  -webkit-print-color-adjust: exact;
  print-color-adjust: exact;
  color: #333;
  background: #fff;
}

/* Text colors */
.text-muted { color: #666; }
.text-primary { color: #0066cc; }
.text-success { color: #28a745; }
.text-warning { color: #856404; }
.text-danger { color: #dc3545; }

/* Background utilities */
.bg-light { background-color: #f8f9fa; }
.bg-white { background-color: #fff; }

/* Alert boxes */
.alert {
  padding: 12px 16px;
  border-radius: 4px;
  margin: 16px 0;
}

.alert-info {
  background-color: #e7f3ff;
  border: 1px solid #b6d4fe;
  color: #084298;
}

.alert-success {
  background-color: #d1e7dd;
  border: 1px solid #badbcc;
  color: #0f5132;
}

.alert-warning {
  background-color: #fff3cd;
  border: 1px solid #ffecb5;
  color: #664d03;
}

.alert-danger {
  background-color: #f8d7da;
  border: 1px solid #f5c2c7;
  color: #842029;
}
```

## Checklist

- [ ] Body has `-webkit-print-color-adjust: exact`
- [ ] pdfParams includes `printBackground: true`
- [ ] Text color is `#666` or darker
- [ ] No transparency/opacity used
- [ ] Gradients replaced with solid colors
- [ ] Tested PDF output for color accuracy
