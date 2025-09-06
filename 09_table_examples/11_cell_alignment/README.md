# Cell Alignment

This lesson shows how to align text, numbers, dates, and status fields in a realistic data table.

## What you'll learn

- How to align **text data** (like names or descriptions).
- How to align **numeric data** (quantities, prices, totals).
- When to use **center alignment** (codes, dates, statuses, actions).
- How to align **column headers** (titles) separately from body cells.
- How vertical alignment works for cells with multiple lines.

## Explanation

- **Headers**

  - In this example, all **column titles are centered** for balance and readability.
  - This makes the header row visually distinct from the body.

- **Left alignment**

  - Best for long text: names, product descriptions, addresses.
  - Matches natural reading flow.

- **Right alignment**

  - Best for numbers: quantities, totals, currency values.
  - Allows easy comparison of digits.

- **Center alignment**

  - Works for short, consistent data:
    - Order IDs or short codes
    - Dates
    - Status values (Pending, Shipped, Cancelled)
    - Icons, checkboxes, or action buttons

- **Vertical alignment**
  - `top` → text sticks to the top (useful for long descriptions).
  - `middle` → default, balances content vertically.
  - `bottom` → rare, but can align values to the bottom edge.

## How to run

Open `index.html` in your browser.  
You’ll see an **order table** with 7 columns:

- **Headers (titles)** → all centered
- **Order ID** → centered
- **Customer** → left aligned
- **Date** → centered
- **Status** → centered
- **Quantity** → right aligned
- **Total** → right aligned
- **Actions** → centered (icons)

## Notes

- Center headers for balance, but align body cells by **content type**.
- Consistent alignment improves readability and scannability.
- For dashboards or reports, follow this rule of thumb:
  - Text → left
  - Numbers → right
  - Codes / Dates / Status / Icons → center
