# PDF Best Practices

Comprehensive guidelines for creating HTML that renders perfectly as PDF documents. This skill helps AI agents and developers create professional, well-formatted PDFs with proper page breaks, margins, and layout.

## Installation

### As an Agent Skill

```bash
npx skills add pdfnoodle/pdf-best-practices
```

### Via npm

```bash
npm install pdf-best-practices
```

## Usage

Start with [SKILL.md](SKILL.md) - it routes you to the right resource based on what you need to do.

### Quick Reference

| Topic | Guide |
| ----- | ----- |
| HTML structure & setup | [Document Setup](resources/document-setup.md) |
| Controlling page breaks | [Page Breaks](resources/page-breaks.md) |
| Table formatting | [Tables](resources/tables.md) |
| Image handling | [Images](resources/images.md) |
| Content optimization | [Content Density](resources/content-density.md) |
| Colors & backgrounds | [Colors](resources/colors.md) |
| Page numbers & headers | [Headers & Footers](resources/headers-footers.md) |
| Invoice, report, certificate, etc. | [Document Types](resources/document-types.md) |

## Key Principles

### Default Configuration

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

### Essential CSS

```css
@page {
  size: A4;
  margin: 40px;
}

body {
  -webkit-print-color-adjust: exact;
  print-color-adjust: exact;
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Arial, sans-serif;
  font-size: 12pt;
  line-height: 1.5;
}

/* Prevent breaks inside content blocks */
.section, figure, tr {
  page-break-inside: avoid;
}

/* Keep headings with content */
h1, h2, h3 {
  page-break-after: avoid;
}
```

## Quick Checklist

Before generating any PDF:

- [ ] Complete HTML structure (DOCTYPE, html, head, body)
- [ ] `@page` rule with A4 size
- [ ] `-webkit-print-color-adjust: exact` on body
- [ ] All images have explicit width/height
- [ ] Tables use thead/tbody structure
- [ ] `page-break-inside: avoid` on content blocks
- [ ] `page-break-after: avoid` on headings
- [ ] No sparse pages (< 25% content)
- [ ] Font sizes 9pt or larger
- [ ] `printBackground: true` in pdfParams

## Works With

- [PDFNoodle](https://pdfnoodle.com) - PDF generation API
- [mcp-server-pdfnoodle](https://github.com/pdfnoodle/mcp-server-pdfnoodle) - MCP server for AI assistants
- Any HTML-to-PDF tool using Puppeteer/Chromium

## License

MIT
