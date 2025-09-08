# HTML Border Attribute vs CSS Borders

This lesson compares the old **HTML `border` attribute** with modern **CSS borders**.

## What you'll learn
- The legacy way: `<table border="1">`
- The modern way: `table { border: 1px solid black; }`
- Why CSS borders are more flexible and recommended.

## Explanation
- **HTML Attribute (`border="1"`)**
  - Quick and simple.
  - Still works in browsers.
  - Deprecated in HTML5 (not recommended for production).
- **CSS Border**
  - Allows full control: thickness, color, style (solid, dashed, dotted, double…).
  - Can be applied differently to the table, rows, or cells.
  - The modern, standards-based approach.

## How to run
Open `index.html` in your browser.  
You’ll see two identical tables: one styled with the old `border` attribute, one styled with CSS.

## Notes
- Use the CSS method for all modern projects.  
- The HTML `border` attribute exists only for backward compatibility.
