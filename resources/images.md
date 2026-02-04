# Images

> Handle images with explicit dimensions and proper positioning for PDF output.

## Golden Rules

1. **Always use absolute URLs** (https://...)
2. **Always specify width and height** in both HTML and CSS
3. **Use `object-fit`** to control aspect ratio
4. **Keep images under 400px height** to fit well on pages
5. **Group images with captions** using `<figure>` elements

## Base Image Styles

```css
img {
  max-width: 100%;
  height: auto;
  page-break-inside: avoid;
}
```

## Size Variants

```css
/* Logo - small fixed size */
.logo {
  width: 150px;
  height: auto;
}

/* Thumbnail */
.thumbnail {
  width: 100px;
  height: 100px;
  object-fit: cover;
}

/* Product image - medium fixed */
.product-image {
  width: 200px;
  height: 200px;
  object-fit: contain;
}

/* Chart or diagram - large */
.chart {
  width: 100%;
  max-width: 500px;
  height: auto;
}

/* Full-width image */
.full-width {
  width: 100%;
  height: auto;
  max-height: 400px;
  object-fit: contain;
}
```

## HTML Best Practices

Always include `width`, `height`, and `alt` attributes:

```html
<img
  src="https://example.com/image.jpg"
  width="300"
  height="200"
  alt="Description of the image"
>
```

## Figures with Captions

Keep images and captions together:

```html
<figure>
  <img
    src="https://example.com/chart.png"
    width="400"
    height="300"
    alt="Q4 Sales Performance Chart"
  >
  <figcaption>Figure 1: Q4 Sales by Region</figcaption>
</figure>
```

```css
figure {
  page-break-inside: avoid;
  break-inside: avoid;
  margin: 20px 0;
  text-align: center;
}

figure img {
  display: block;
  margin: 0 auto;
}

figcaption {
  margin-top: 8px;
  font-size: 10pt;
  color: #666;
  font-style: italic;
}
```

## Image Galleries

For multiple images in a row:

```html
<div class="image-gallery">
  <figure>
    <img src="img1.jpg" width="200" height="150" alt="Image 1">
    <figcaption>Caption 1</figcaption>
  </figure>
  <figure>
    <img src="img2.jpg" width="200" height="150" alt="Image 2">
    <figcaption>Caption 2</figcaption>
  </figure>
  <figure>
    <img src="img3.jpg" width="200" height="150" alt="Image 3">
    <figcaption>Caption 3</figcaption>
  </figure>
</div>
```

```css
.image-gallery {
  display: flex;
  flex-wrap: wrap;
  gap: 20px;
  justify-content: center;
  page-break-inside: avoid;
}

.image-gallery figure {
  flex: 0 0 auto;
  margin: 0;
}
```

## Object-Fit Reference

| Value | Behavior |
| ----- | -------- |
| `contain` | Scale to fit, preserve aspect ratio, may have empty space |
| `cover` | Scale to fill, preserve aspect ratio, may crop |
| `fill` | Stretch to fill, may distort |
| `none` | No scaling, may overflow |
| `scale-down` | Like `contain` but never scales up |

## Background Images

For decorative background images:

```css
.hero-section {
  background-image: url('https://example.com/bg.jpg');
  background-size: cover;
  background-position: center;
  -webkit-print-color-adjust: exact;
  print-color-adjust: exact;
}
```

**Note:** Requires `printBackground: true` in PDF parameters.

## Common Issues

| Problem | Solution |
| ------- | -------- |
| Image not showing | Use absolute URL (https://...) |
| Image stretched/distorted | Add `object-fit: contain` |
| Image too large for page | Set `max-height: 400px` |
| Image split across pages | Add `page-break-inside: avoid` to figure |
| Caption separated from image | Wrap in `<figure>` with `page-break-inside: avoid` |
| Blurry images | Use higher resolution source (2x for retina) |

## Complete Example

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    img {
      max-width: 100%;
      height: auto;
    }

    figure {
      page-break-inside: avoid;
      break-inside: avoid;
      margin: 20px 0;
      text-align: center;
    }

    figcaption {
      margin-top: 8px;
      font-size: 10pt;
      color: #666;
    }

    .logo { width: 120px; }
    .product { width: 200px; height: 200px; object-fit: contain; }
    .chart { width: 100%; max-height: 400px; }
  </style>
</head>
<body>
  <img src="https://example.com/logo.png" class="logo" alt="Company Logo">

  <figure>
    <img
      src="https://example.com/product.jpg"
      class="product"
      width="200"
      height="200"
      alt="Product Photo"
    >
    <figcaption>Figure 1: Product XYZ</figcaption>
  </figure>
</body>
</html>
```
