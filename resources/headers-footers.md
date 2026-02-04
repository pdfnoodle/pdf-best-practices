# Headers & Footers

> Add document headers, page numbers, and running footers to PDFs.

## Two Types of Headers/Footers

1. **Document headers** - Part of your HTML content (letterhead, title blocks)
2. **Page headers/footers** - Added by PDF engine on every page (page numbers)

## Document Headers

### Basic Header

```html
<header class="document-header">
  <img src="https://example.com/logo.png" class="logo" alt="Company Logo">
  <div class="header-text">
    <h1>Document Title</h1>
    <p class="subtitle">Subtitle or description</p>
  </div>
</header>
```

```css
.document-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding-bottom: 20px;
  border-bottom: 2px solid #333;
  margin-bottom: 30px;
}

.document-header .logo {
  width: 120px;
  height: auto;
}

.document-header h1 {
  margin: 0;
  font-size: 28pt;
}

.document-header .subtitle {
  margin: 4px 0 0 0;
  color: #666;
}
```

### Letterhead Style

```html
<header class="letterhead">
  <div class="company-info">
    <img src="logo.png" width="100" alt="Logo">
    <div>
      <strong>Company Name</strong><br>
      123 Business St, City, State 12345<br>
      (555) 123-4567 | email@company.com
    </div>
  </div>
  <div class="document-info">
    <strong>Invoice #1234</strong><br>
    Date: January 15, 2025
  </div>
</header>
```

```css
.letterhead {
  display: flex;
  justify-content: space-between;
  margin-bottom: 40px;
  padding-bottom: 20px;
  border-bottom: 1px solid #ddd;
}

.company-info {
  display: flex;
  gap: 16px;
  align-items: center;
}

.document-info {
  text-align: right;
}
```

## Page Headers/Footers (via pdfParams)

Use `headerTemplate` and `footerTemplate` in PDF parameters for repeating elements on every page.

### Page Numbers Only

```json
{
  "format": "A4",
  "margin": {
    "top": "60px",
    "right": "40px",
    "bottom": "60px",
    "left": "40px"
  },
  "displayHeaderFooter": true,
  "headerTemplate": "<div></div>",
  "footerTemplate": "<div style='font-size: 10px; width: 100%; text-align: center; color: #666;'>Page <span class='pageNumber'></span> of <span class='totalPages'></span></div>"
}
```

### Header with Title + Footer with Page Numbers

```json
{
  "displayHeaderFooter": true,
  "headerTemplate": "<div style='font-size: 10px; width: 100%; text-align: center; color: #666; border-bottom: 1px solid #ddd; padding-bottom: 5px;'>Document Title</div>",
  "footerTemplate": "<div style='font-size: 10px; width: 100%; text-align: center; color: #666;'>Page <span class='pageNumber'></span> of <span class='totalPages'></span></div>"
}
```

### Available Template Variables

| Variable | Description |
| -------- | ----------- |
| `<span class='pageNumber'></span>` | Current page number |
| `<span class='totalPages'></span>` | Total page count |
| `<span class='date'></span>` | Current date |
| `<span class='title'></span>` | Document title |
| `<span class='url'></span>` | Document URL |

### Styled Footer Example

```json
{
  "footerTemplate": "<div style='font-size: 9px; width: 100%; padding: 0 40px; display: flex; justify-content: space-between; color: #666;'><span>Company Name</span><span>Page <span class='pageNumber'></span> of <span class='totalPages'></span></span><span>Confidential</span></div>"
}
```

## Important Notes

### Margin Requirements

Header and footer templates render **inside** the margins. Increase margins to accommodate them:

```json
{
  "margin": {
    "top": "80px",
    "bottom": "80px"
  }
}
```

### Template Styling Limitations

- Templates are rendered separately from your HTML
- They cannot access your document's CSS
- All styles must be inline
- Keep templates simple

### Cover Pages

Use `hasCover: true` to hide header/footer on the first page:

```json
{
  "hasCover": true,
  "displayHeaderFooter": true,
  "headerTemplate": "...",
  "footerTemplate": "..."
}
```

## Document Footers

For footers that are part of your document content (not repeated per page):

```html
<footer class="document-footer">
  <p>Terms and conditions apply. See website for details.</p>
  <p>© 2025 Company Name. All rights reserved.</p>
</footer>
```

```css
.document-footer {
  margin-top: 40px;
  padding-top: 20px;
  border-top: 1px solid #ddd;
  font-size: 10pt;
  color: #666;
  text-align: center;
}
```

## Complete Example

```json
{
  "format": "A4",
  "margin": {
    "top": "70px",
    "right": "40px",
    "bottom": "70px",
    "left": "40px"
  },
  "printBackground": true,
  "displayHeaderFooter": true,
  "headerTemplate": "<div style='font-size: 9px; width: 100%; text-align: right; color: #999; padding-right: 40px;'>CONFIDENTIAL</div>",
  "footerTemplate": "<div style='font-size: 9px; width: 100%; padding: 0 40px; display: flex; justify-content: space-between; color: #666;'><span>Generated on <span class='date'></span></span><span>Page <span class='pageNumber'></span> of <span class='totalPages'></span></span></div>"
}
```

## Checklist

- [ ] Document header styled and positioned
- [ ] Margins increased if using page headers/footers (60-80px)
- [ ] `displayHeaderFooter: true` if using templates
- [ ] Templates use inline styles only
- [ ] `hasCover: true` if first page should skip headers/footers
- [ ] Footer includes page numbers for multi-page docs
