# `inline-size: max-content` + `max-inline-size: 100%` — Responsive Shrink‑Wrap

**What this demo is**

A 2‑column table whose tracks are defined via `<colgroup>` (**150px / 350px**). It uses **logical sizing** to shrink‑wrap to its intrinsic width (\~500px) but also **caps** that width so it won’t overflow small screens:

```css
 table {
   border-collapse: collapse;
   inline-size: max-content; /* shrink-wrap to intrinsic width (≈150+350) */
   max-inline-size: 100%;    /* cap at container width (responsive) */
   table-layout: fixed;      /* honor <colgroup> track sizes */
 }
```

The focus here is the **combination** of `inline-size: max-content` (shrink‑wrap) with `max-inline-size: 100%` (responsive cap).

---

## Why this combo is useful

* **Shrink‑wrap by default**: On wide viewports, the table sizes to the sum of its tracks (\~500px), just like a precise, fixed‑width component.
* **Responsively caps**: On narrow screens, the table never exceeds its container; it **shrinks to fit** (up to the limits of its fixed tracks) instead of causing horizontal overflow.
* **Keeps block formatting**: Unlike `display: inline-table`, you retain block‑level behavior and semantics.

---

## How it behaves

* With `table-layout: fixed` + `<colgroup>`, columns remain **authoritative** at **150px / 350px**.
* `inline-size: max-content` asks for the **intrinsic width** (≈ 500px + borders).
* `max-inline-size: 100%` prevents overflow; if the container is narrower than 500px, the table’s inline size is **clamped** to fit.
* Because tracks are fixed, text wraps **inside** the columns. Keeping `overflow-wrap: anywhere;` ensures even unbroken tokens don’t force overflow.

> Note: When clamped smaller than the track sum, browsers still keep the fixed track proportions but will **wrap content more aggressively**. Replaced elements (images) should be constrained (`max-width:100%`).

---

## When to use it

* You want a table that’s **exact‑width** on desktop but **gracefully fits** smaller containers without manual breakpoints.
* You prefer **logical properties** for writing‑mode friendliness (LTR/RTL/vertical).
* You don’t want to hard‑code a `width` nor switch to `inline-table`.

---

## Comparisons

| Approach                                                  | Behavior                                        | Notes                                |
| --------------------------------------------------------- | ----------------------------------------------- | ------------------------------------ |
| `width: 500px;`                                           | Always 500px (can overflow on small screens)    | Not responsive by itself             |
| `display: inline-table;`                                  | Shrink‑wraps to tracks; inline‑level formatting | Changes formatting context           |
| `inline-size: max-content;`                               | Shrink‑wraps; may overflow on narrow screens    | Add a cap                            |
| **`inline-size: max-content;` + `max-inline-size: 100%`** | Shrink‑wrap **and** responsive cap              | Block formatting; writing‑mode aware |

---

## Practical tips

* **Center the table** (block formatting preserved):

  ```css
  table { margin-inline: auto; }
  ```
* **Guard rails for content**:

  ```css
  th, td { overflow-wrap: anywhere; }
  td img { max-width: 100%; height: auto; }
  ```
* **Scrollable container fallback** (if your design prefers fixed tracks without reflow):

  ```css
  .table-wrapper { overflow-x: auto; }
  .table-wrapper > table { inline-size: max-content; }
  ```

---

## Key CSS (from this demo)

```css
table {
  border-collapse: collapse;
  inline-size: max-content; /* shrink-wrap to tracks (~500px) */
  max-inline-size: 100%;    /* responsive cap */
  table-layout: fixed;      /* respect <colgroup> widths */
}
th, td { border: 1px solid #444; overflow-wrap: anywhere; }
.col-1 { width: 150px; }
.col-2 { width: 350px; }
```

**Takeaway**

Pair **`inline-size: max-content`** with **`max-inline-size: 100%`** to get the best of both worlds: a table that **shrink‑wraps** to precise tracks on large screens yet **doesn’t overflow** on small ones—no hard‑coded widths, no inline formatting side effects.
