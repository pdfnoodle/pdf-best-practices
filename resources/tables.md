# Tables

> Format tables for clean rendering across multiple PDF pages.

## Base Table Styles

```css
table {
  width: 100%;
  border-collapse: collapse;
  margin: 16px 0;
  font-size: 11pt;
  table-layout: fixed;
  word-wrap: break-word;
}

th, td {
  border: 1px solid #ddd;
  padding: 8px 12px;
  text-align: left;
  vertical-align: top;
}

th {
  background-color: #f5f5f5;
  font-weight: 600;
}

/* Zebra striping for readability */
tbody tr:nth-child(even) {
  background-color: #fafafa;
}

/* Prevent row breaks */
tr {
  page-break-inside: avoid;
  break-inside: avoid;
}
```

## Table Structure

Always use proper `thead` and `tbody` structure for multi-page tables:

```html
<table>
  <thead>
    <tr>
      <th>Column 1</th>
      <th>Column 2</th>
      <th>Column 3</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Data 1</td>
      <td>Data 2</td>
      <td>Data 3</td>
    </tr>
    <!-- More rows -->
  </tbody>
</table>
```

**Why?** The `thead` element allows PDF engines to repeat headers on each page when tables span multiple pages.

## Column Width Control

Use fixed widths for consistent column sizing:

```css
/* By percentage */
table.invoice-items th:nth-child(1) { width: 50%; }
table.invoice-items th:nth-child(2) { width: 15%; }
table.invoice-items th:nth-child(3) { width: 15%; }
table.invoice-items th:nth-child(4) { width: 20%; }

/* Or by pixels */
table.data-table th:nth-child(1) { width: 200px; }
table.data-table th:nth-child(2) { width: 100px; }
```

## Alignment Patterns

```css
/* Right-align numbers and currency */
.text-right,
td.amount,
td.number,
td.currency {
  text-align: right;
}

/* Center-align status or short values */
.text-center,
td.status,
td.checkbox {
  text-align: center;
}
```

## Table Variants

### Compact Table

```css
table.compact th,
table.compact td {
  padding: 4px 8px;
  font-size: 10pt;
}
```

### Borderless Table

```css
table.borderless,
table.borderless th,
table.borderless td {
  border: none;
}

table.borderless th {
  border-bottom: 2px solid #333;
}
```

### Striped Table

```css
table.striped tbody tr:nth-child(odd) {
  background-color: #fff;
}

table.striped tbody tr:nth-child(even) {
  background-color: #f9f9f9;
}
```

## Summary Rows

Keep summary/total rows with the table body:

```html
<table>
  <thead>
    <tr>
      <th>Item</th>
      <th>Amount</th>
    </tr>
  </thead>
  <tbody>
    <tr><td>Product A</td><td>$100</td></tr>
    <tr><td>Product B</td><td>$200</td></tr>
  </tbody>
  <tfoot>
    <tr class="total-row">
      <td><strong>Total</strong></td>
      <td><strong>$300</strong></td>
    </tr>
  </tfoot>
</table>
```

```css
tfoot .total-row {
  page-break-inside: avoid;
  break-inside: avoid;
  background-color: #f0f0f0;
  font-weight: bold;
}
```

## Wide Tables

For tables with many columns:

1. **Reduce font size** (minimum 9pt)
2. **Use landscape orientation** if needed
3. **Split into multiple tables** by column groups
4. **Abbreviate headers** where possible

```css
table.wide {
  font-size: 9pt;
}

table.wide th,
table.wide td {
  padding: 4px 6px;
}
```

## Complete Example

```css
/* Full table styling system */
table {
  width: 100%;
  border-collapse: collapse;
  margin: 16px 0;
  font-size: 11pt;
  table-layout: fixed;
  word-wrap: break-word;
}

th, td {
  border: 1px solid #ddd;
  padding: 8px 12px;
  text-align: left;
  vertical-align: top;
}

th {
  background-color: #f5f5f5;
  font-weight: 600;
}

tbody tr:nth-child(even) {
  background-color: #fafafa;
}

tr {
  page-break-inside: avoid;
  break-inside: avoid;
}

tfoot td {
  background-color: #f0f0f0;
  font-weight: bold;
  border-top: 2px solid #333;
}

/* Alignment utilities */
.text-right { text-align: right; }
.text-center { text-align: center; }
```
