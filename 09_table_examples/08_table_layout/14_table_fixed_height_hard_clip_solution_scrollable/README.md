# Fixed Row Height — Minimal Scroll-In-Cell

**What this demo is**

A 2×2 table that preserves real table cells but places **an inner `<div>` in each cell** with a fixed height (40px) and `overflow: auto`. When content exceeds 40px, the inner area **scrolls** instead of growing the row.

**What you will see**

- Rows look about **41px** tall (≈ 40px content + \~1px collapsed border).
- Short text shows normally; **long text becomes scrollable** inside the cell.
- Table semantics stay intact: column alignment, `<colgroup>`, and collapsed borders all work.

**Why it behaves like this**

- The height/overflow rules live on the **inner wrapper**, not the `<td>/<th>` themselves.
- `overflow: auto` only shows scrollbars **if needed**, so simple cells remain clean.

**When to use this pattern**

- You need a **strict, uniform row height** but must keep **all content accessible** without growing the table.
- Good for dense tables where expansion would break layout, yet truncation isn’t acceptable.

**Limitations**

- **In‑cell scrolling** can be hard to discover and awkward for keyboard users; consider adding a visible cue.
- Mobile/touch scrolling inside cells can feel cramped.
- Printing/export may not honor the scroll area; verify if you need hard copies.

**Key CSS used**

```css
th,
td {
  border: 1px solid #444;
  padding: 0; /* move padding to inner div */
}

th > div,
td > div {
  height: 40px; /* fixed visual height */
  overflow: auto; /* scroll only when needed */
  white-space: normal; /* allow wrapping */
  padding: 0 8px; /* inner padding */
  box-sizing: border-box;
}
```

**Takeaway**

Choose **scroll-in-cell** when you must enforce a fixed row height **and** keep full text available, accepting the UX trade‑offs of a tiny scroll area.
