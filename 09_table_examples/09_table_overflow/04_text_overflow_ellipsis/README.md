# Text Overflow in Tables — `clip` vs `hidden` vs `ellipsis`

**What this demo is**

A 3‑column table (equal tracks, fixed layout) illustrating how `text-overflow` works in table cells when combined with `white-space` and `overflow`:

* **Normal Wrap** — multi‑line wrapping (`white-space: normal; text-overflow: clip;`).
* **Hidden Overflow** — single line, clipped tail (`white-space: nowrap; overflow: hidden; text-overflow: clip;`).
* **Ellipsis** — single line, clipped tail with `…` (`white-space: nowrap; overflow: hidden; text-overflow: ellipsis;`).

`table-layout: fixed` gives predictable column widths so truncation happens exactly at the cell boundary.

---

## How `text-overflow` really works

`text-overflow` **does nothing by itself**. For the ellipsis to appear:

1. The text must be **constrained** by a width (via `table-layout: fixed`, an explicit `width`, or an inner wrapper width).
2. The content must be on **a single line** → `white-space: nowrap;`
3. The overflow must be **clipped** → `overflow: hidden;` *(or `clip`)*
4. The rendering box should generate an inline formatting context (block/inline‑block, table cell is fine).

Only then does `text-overflow: ellipsis;` show the `…` when the text exceeds the box.

---

## What each column shows

### 1) Normal Wrap

* `white-space: normal; text-overflow: clip;`
* Lines wrap naturally; **no ellipsis** because the text isn’t clipped horizontally.
* Good when preserving all text is more important than uniform row height.

### 2) Hidden Overflow (no ellipsis)

* `white-space: nowrap; overflow: hidden; text-overflow: clip;`
* Keeps one line and **clips** excess characters **without** a visual cue.
* Useful only as a diagnostic or when you add your own cue (e.g., tooltip).

### 3) Ellipsis

* `white-space: nowrap; overflow: hidden; text-overflow: ellipsis;`
* Single‑line truncation with a clear visual cue (`…`).
* Great for dense tables with short labels/IDs.

---

## Multiline truncation (not in this demo)

`text-overflow: ellipsis` is **single‑line only**. For multiple lines, use a wrapper and a clamping pattern:

```html
<td>
  <div class="clamp2">Very long text …</div>
</td>
```

```css
.clamp2{display:-webkit-box;-webkit-line-clamp:2;-webkit-box-orient:vertical;overflow:hidden}
```

**Notes**

* Works widely in modern browsers (WebKit/Blink/Chromium, recent Firefox behind logical equivalents for line clamp).
* Avoid putting the clamp directly on `<td>`; use an **inner wrapper** to keep table layout stable.

---

## Interactions & gotchas

* **`table-layout: fixed`** keeps columns stable so truncation is consistent. With auto layout, columns may widen and defeat truncation.
* **`overflow-wrap:anywhere`** competes with single‑line truncation: it will insert breaks; if you want ellipsis, keep `nowrap`.
* **Intrinsic media** (images/iframes) won’t obey text ellipsis; constrain with `max-width:100%` or wrap text in an inner element.
* **Ellipsis width** is part of the rendering; extremely narrow cells may still show partial characters.

---

## Practical recipes

**A) One‑line label with ellipsis**

```css
.cell-1l{white-space:nowrap;overflow:hidden;text-overflow:ellipsis}
```

**B) Header cells with consistent truncation**

```css
th{white-space:nowrap}
th>span{display:block;overflow:hidden;text-overflow:ellipsis}
```

**C) Multiline clamp with safe fallback**

```css
.cell-2l{display:-webkit-box;-webkit-line-clamp:2;-webkit-box-orient:vertical;overflow:hidden}
@supports not (-webkit-line-clamp:2){.cell-2l{white-space:nowrap;overflow:hidden;text-overflow:ellipsis}}
```

**D) Reveal full text on hover (pure CSS tooltip)**

```css
.cell-1l[title]{cursor:help}
```

*(Set the cell’s `title` attribute from your data so users can see the full value.)*

---

## Key CSS in this demo

```css
table{border-collapse:collapse;width:800px;table-layout:fixed}
th,td{border:1px solid #444;padding:8px;vertical-align:top;width:33%}

/* Multi-line wrap */
td.wrap{white-space:normal;text-overflow:clip}

/* Single line clipped */
td.hidden{white-space:nowrap;overflow:hidden;text-overflow:clip}

/* Single line with ellipsis */
td.ellipsis{white-space:nowrap;overflow:hidden;text-overflow:ellipsis}
```

**Takeaway**

Use **ellipsis** for compact, single‑line cells; use **wrapping** when completeness beats density; use **line‑clamp wrappers** for elegant multi‑line truncation. Keep columns deterministic (`table-layout: fixed`) so truncation behaves predictably.
