# Document Types

> Type-specific guidelines for common PDF document formats.

## Invoice

### Key Principles
- Keep entire invoice on one page if possible
- Clear visual hierarchy: header → details → line items → totals
- Right-align all monetary values
- Include payment terms prominently

### Structure

```html
<div class="invoice">
  <header class="invoice-header">
    <div class="company">
      <img src="logo.png" width="120" alt="Logo">
      <address>Company Name<br>Address Line 1<br>City, State ZIP</address>
    </div>
    <div class="invoice-details">
      <h1>INVOICE</h1>
      <p>Invoice #: 1234</p>
      <p>Date: January 15, 2025</p>
      <p>Due: February 15, 2025</p>
    </div>
  </header>

  <section class="bill-to">
    <h3>Bill To:</h3>
    <address>Client Name<br>Address</address>
  </section>

  <table class="line-items">
    <thead>
      <tr>
        <th>Description</th>
        <th>Qty</th>
        <th>Unit Price</th>
        <th>Amount</th>
      </tr>
    </thead>
    <tbody>
      <tr><td>Service A</td><td>1</td><td>$100.00</td><td>$100.00</td></tr>
    </tbody>
    <tfoot>
      <tr><td colspan="3">Subtotal</td><td>$100.00</td></tr>
      <tr><td colspan="3">Tax (10%)</td><td>$10.00</td></tr>
      <tr class="total"><td colspan="3"><strong>Total</strong></td><td><strong>$110.00</strong></td></tr>
    </tfoot>
  </table>

  <footer class="payment-terms">
    <p><strong>Payment Terms:</strong> Net 30</p>
    <p>Make checks payable to: Company Name</p>
  </footer>
</div>
```

### CSS Tips

```css
.invoice { font-size: 11pt; }
.line-items th:nth-child(1) { width: 50%; }
.line-items th:nth-child(2) { width: 10%; text-align: center; }
.line-items th:nth-child(3) { width: 20%; text-align: right; }
.line-items th:nth-child(4) { width: 20%; text-align: right; }
.line-items td:nth-child(2) { text-align: center; }
.line-items td:nth-child(3),
.line-items td:nth-child(4) { text-align: right; }
.total td { border-top: 2px solid #333; }
```

---

## Report

### Key Principles
- Title page with document info
- Table of contents for 3+ pages
- Consistent heading hierarchy
- Page breaks before major sections
- Executive summary at start

### Structure

```html
<!-- Title Page -->
<div class="title-page">
  <h1>Report Title</h1>
  <p class="subtitle">Subtitle or Description</p>
  <p class="meta">
    Prepared by: Author Name<br>
    Date: January 15, 2025<br>
    Version: 1.0
  </p>
</div>

<!-- Table of Contents -->
<div class="toc page-break-before">
  <h2>Table of Contents</h2>
  <ol>
    <li><a href="#exec-summary">Executive Summary</a></li>
    <li><a href="#section-1">Section 1: Analysis</a></li>
    <li><a href="#section-2">Section 2: Findings</a></li>
    <li><a href="#conclusion">Conclusion</a></li>
  </ol>
</div>

<!-- Content -->
<section id="exec-summary" class="page-break-before">
  <h2>Executive Summary</h2>
  <p>Key findings and recommendations...</p>
</section>

<section id="section-1" class="page-break-before">
  <h2>Section 1: Analysis</h2>
  <h3>1.1 Background</h3>
  <p>Content...</p>
</section>
```

### CSS Tips

```css
.title-page {
  text-align: center;
  padding-top: 200px;
}

.title-page h1 {
  font-size: 36pt;
  margin-bottom: 20px;
}

.toc ol {
  list-style-type: decimal;
  padding-left: 24px;
}

.toc li {
  margin: 8px 0;
}

section {
  page-break-before: always;
}

section:first-of-type {
  page-break-before: auto;
}
```

---

## Certificate

### Key Principles
- Center all content
- Elegant, larger fonts (18-36pt)
- Decorative borders
- Single page only
- Consider landscape orientation

### Structure

```html
<div class="certificate">
  <div class="border-outer">
    <div class="border-inner">
      <div class="certificate-content">
        <p class="header-text">Certificate of Completion</p>
        <p class="presented">This is to certify that</p>
        <p class="recipient">John Smith</p>
        <p class="achievement">has successfully completed the</p>
        <p class="course">Advanced Web Development Course</p>
        <p class="date">January 15, 2025</p>

        <div class="signatures">
          <div class="signature">
            <div class="line"></div>
            <p>Instructor</p>
          </div>
          <div class="signature">
            <div class="line"></div>
            <p>Director</p>
          </div>
        </div>
      </div>
    </div>
  </div>
</div>
```

### CSS Tips

```css
.certificate {
  text-align: center;
  padding: 20px;
}

.border-outer {
  border: 3px solid #333;
  padding: 10px;
}

.border-inner {
  border: 1px solid #666;
  padding: 40px;
}

.header-text {
  font-size: 36pt;
  font-weight: bold;
  color: #333;
  margin-bottom: 30px;
}

.recipient {
  font-size: 28pt;
  font-style: italic;
  margin: 20px 0;
}

.signatures {
  display: flex;
  justify-content: center;
  gap: 100px;
  margin-top: 60px;
}

.signature .line {
  width: 150px;
  border-bottom: 1px solid #333;
  margin-bottom: 8px;
}
```

### PDF Params for Landscape

```json
{
  "format": "A4",
  "landscape": true,
  "margin": { "top": "40px", "right": "40px", "bottom": "40px", "left": "40px" }
}
```

---

## Letter

### Key Principles
- Standard business letter format
- Letterhead with logo and address
- Clear date and recipient block
- Signature area at bottom
- 1-2 pages maximum

### Structure

```html
<div class="letter">
  <header class="letterhead">
    <img src="logo.png" width="100" alt="Logo">
    <div class="company-address">
      Company Name<br>
      123 Business Street<br>
      City, State 12345<br>
      (555) 123-4567
    </div>
  </header>

  <p class="date">January 15, 2025</p>

  <div class="recipient">
    <p>Mr. John Smith</p>
    <p>Position Title</p>
    <p>Company Name</p>
    <p>456 Client Street</p>
    <p>City, State 67890</p>
  </div>

  <p class="salutation">Dear Mr. Smith,</p>

  <div class="body">
    <p>First paragraph introducing the purpose of the letter...</p>
    <p>Body paragraphs with main content...</p>
    <p>Closing paragraph with next steps or call to action...</p>
  </div>

  <div class="closing">
    <p>Sincerely,</p>
    <div class="signature-space"></div>
    <p class="sender-name">Jane Doe</p>
    <p class="sender-title">Director of Operations</p>
  </div>
</div>
```

### CSS Tips

```css
.letterhead {
  display: flex;
  justify-content: space-between;
  margin-bottom: 40px;
}

.date {
  margin: 30px 0;
}

.recipient {
  margin-bottom: 30px;
  line-height: 1.4;
}

.salutation {
  margin-bottom: 20px;
}

.body p {
  margin-bottom: 16px;
  text-align: justify;
}

.closing {
  margin-top: 30px;
}

.signature-space {
  height: 60px;
}

.sender-name {
  font-weight: bold;
}
```

---

## Table-Heavy Document

### Key Principles
- Smaller font size (10-11pt)
- Header rows repeat on each page
- Fixed column widths
- Zebra striping for readability
- Summary rows stay with data

### CSS Tips

```css
table {
  font-size: 10pt;
  width: 100%;
}

th, td {
  padding: 6px 8px;
}

thead {
  display: table-header-group;  /* Repeat on pages */
}

tbody tr:nth-child(even) {
  background-color: #f9f9f9;
}

tr {
  page-break-inside: avoid;
}
```

---

## Image-Heavy Document

### Key Principles
- Set max image height (300-400px)
- Use figure + figcaption
- Prevent images breaking across pages
- Consider 2-3 images per row for galleries
- Optimize image file sizes

### CSS Tips

```css
figure {
  page-break-inside: avoid;
  break-inside: avoid;
  margin: 20px 0;
}

img {
  max-width: 100%;
  max-height: 350px;
  object-fit: contain;
}

.gallery {
  display: flex;
  flex-wrap: wrap;
  gap: 16px;
  justify-content: center;
}

.gallery figure {
  flex: 0 0 calc(50% - 8px);
  margin: 0;
}
```
