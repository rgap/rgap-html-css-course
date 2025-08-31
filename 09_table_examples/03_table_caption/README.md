# Lesson 03 – Table Caption

This lesson introduces the `<caption>` element for tables.

## What you'll learn

- How to add a **title** to a table using `<caption>`.
- Default behavior: captions appear **above the table**.
- Captions improve **accessibility** by describing the table’s purpose.

## Explanation

- `<caption>` must be the **first child** of `<table>`.
- It is read by screen readers as the table’s description.
- Captions can be styled with CSS (`caption-side: top|bottom`, fonts, colors).

## How to run

Open `index.html` in your browser.  
You’ll see a table with a title ("Inventory Summary – August") above it.

## Notes

- The default placement is at the top, but you can move it to the bottom with CSS:
  ```css
  caption {
    caption-side: bottom;
  }
  ```
