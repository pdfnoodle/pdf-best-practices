# Document Setup

> Essential HTML structure and CSS setup for PDF-ready documents.

## Required HTML Structure

Always wrap your content in a complete HTML document:

```html
<!DOCTYPE html>
<html>
<head>
  <meta charset="UTF-8">
  <style>
    /* Your styles here */
  </style>
</head>
<body>
  <!-- Your content here -->
</body>
</html>
```

## Base CSS Template

```css
@page {
  size: A4;
  margin: 40px;
}

* {
  box-sizing: border-box;
}

html, body {
  margin: 0;
  padding: 0;
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, 'Helvetica Neue', Arial, sans-serif;
  font-size: 12pt;
  line-height: 1.5;
  color: #333;
}

body {
  width: 100%;
  max-width: 100%;
  -webkit-print-color-adjust: exact;
  print-color-adjust: exact;
}
```

## A4 Paper Specifications

| Property | Value |
| -------- | ----- |
| Width | 210mm (794px at 96 DPI) |
| Height | 297mm (1123px at 96 DPI) |
| Safe content width (40px margins) | ~714px |
| Safe content height per page (40px margins) | ~1043px |

## PDF Parameters

When calling the PDF generation API, use these defaults:

```json
{
  "format": "A4",
  "margin": {
    "top": "40px",
    "right": "40px",
    "bottom": "40px",
    "left": "40px"
  },
  "printBackground": true
}
```

### Parameter Reference

| Parameter | Type | Description |
| --------- | ---- | ----------- |
| `format` | string | Paper size: "A4", "Letter", "Legal", etc. |
| `margin` | object | Page margins with top, right, bottom, left |
| `printBackground` | boolean | Include CSS backgrounds in output |
| `landscape` | boolean | Landscape orientation (default: false) |
| `displayHeaderFooter` | boolean | Show header/footer templates |
| `headerTemplate` | string | HTML template for page headers |
| `footerTemplate` | string | HTML template for page footers |

## Typography Defaults

```css
/* Recommended font sizes */
h1 { font-size: 24pt; margin: 0 0 16px 0; }
h2 { font-size: 18pt; margin: 24px 0 12px 0; }
h3 { font-size: 14pt; margin: 20px 0 10px 0; }

p, li, td { font-size: 12pt; }
small, .caption { font-size: 10pt; }

/* Never go below 9pt for body text */
```

## Complete Starter Template

```html
<!DOCTYPE html>
<html>
<head>
  <meta charset="UTF-8">
  <style>
    @page {
      size: A4;
      margin: 40px;
    }

    * {
      box-sizing: border-box;
    }

    html, body {
      margin: 0;
      padding: 0;
      font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Arial, sans-serif;
      font-size: 12pt;
      line-height: 1.5;
      color: #333;
    }

    body {
      -webkit-print-color-adjust: exact;
      print-color-adjust: exact;
    }

    h1 { font-size: 24pt; margin: 0 0 20px 0; }
    h2 { font-size: 18pt; margin: 30px 0 15px 0; }
    h3 { font-size: 14pt; margin: 20px 0 10px 0; }

    p {
      margin: 0 0 12px 0;
    }

    h1, h2, h3 {
      page-break-after: avoid;
      break-after: avoid;
    }
  </style>
</head>
<body>
  <h1>Document Title</h1>
  <p>Your content here...</p>
</body>
</html>
```
