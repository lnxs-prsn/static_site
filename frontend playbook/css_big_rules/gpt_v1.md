
---

# 🧠 1. The Cascade (who wins?)

CSS is not just “instructions”, it’s a **conflict resolver**.

When multiple rules apply:

> CSS decides which one wins

Based on:

* specificity (`.class` vs `div`)
* order (later wins)
* importance (`!important`)

### Mental model:

> “many rules compete → one survives”

---

# 📦 2. The Box Model (everything is a box)

Every element is a rectangle:

```text id="box"
content → padding → border → margin
```

So when you see a “thing on screen”:

> it is always a box, never just text or shape

This is why backgrounds, spacing, and borders behave consistently.

---

# 🧱 3. Layout Systems (your discovery)

This is your current insight:

> layout engine decides size → then placement

Includes:

* Grid
* Flexbox
* Block layout

### Mental model:

> “how elements are arranged in space”

---

# 🎨 4. Painting (how things look)

After layout is decided:

> CSS “paints” visuals on top

Includes:

* color
* background
* shadows
* borders

Important:

> painting does NOT affect layout

---

# 📐 5. Inheritance (who passes properties down)

Some properties automatically flow:

Example:

```css id="inh"
font-family
color
```

So:

> parent can control children without targeting them

But others do NOT inherit:

* margin
* padding
* width

---

# ⚡ 6. Default behavior (the “hidden CSS”)

Every element already has CSS rules:

* `div` → display: block
* `span` → display: inline
* `body` → margin: 8px (default browser style)

So CSS is always:

> “your rules + browser rules”

---

# 🔥 7. Containing context (important for Grid/Flex)

Some properties only work if parent enables a system:

* `justify-items` → only works in grid
* `justify-content` → depends on layout type
* `position: absolute` → depends on nearest positioned parent

---

# 🧠 Putting it all together (the real mental model)

CSS is not one rule.

It is 5 systems working together:

```
1. Cascade (which rule wins)
2. Box Model (what is the shape)
3. Layout (where it goes)
4. Painting (how it looks)
5. Inheritance (what gets passed down)
```

---