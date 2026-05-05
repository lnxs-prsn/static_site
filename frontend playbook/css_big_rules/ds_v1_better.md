
> *Sizing and alignment are two separate steps. First change how the box *sizes* (stretch → shrink), *then* align that result.*

That’s a perfect insight. Let me give you the other **big, simple rules** — explained for someone who is *not* an expert.

---

## Big Rule #2: Everything is a box inside a box

Every HTML element is a rectangular box.  
Inside that box you have:  
**content** → **padding** (inside space) → **border** → **margin** (outside space)

The **total width** of the box = content + padding + border.  
(Margin adds space *outside* the box.)

**What trips people up:**  
If you set `width: 200px`, you’re only setting the *content* width. Add padding and border, and the box gets wider than 200px.

**Fix:** Use `box-sizing: border-box` — then `width: 200px` means *total* width, padding and border included.

---

## Big Rule #3: Two kinds of elements – block vs inline

- **Block elements** (like `<div>`, `<p>`, `<h1>`):  
  They *stretch* to fill the whole width of their parent.  
  They start on a new line.

- **Inline elements** (like `<span>`, `<a>`, `<strong>`):  
  They *shrink* to fit their content.  
  They sit side‑by‑side, like words in a sentence.

**What trips people up:**  
You try to set `width` or `margin-top` on an inline element — it does nothing.

**Fix:** Change it to `display: inline-block` or `display: block`.

---

## Big Rule #4: Percentage sizes look at the *parent*, not always the way you expect

- `width: 50%` → 50% of the parent’s **width**.
- `height: 50%` → only works if the parent has a **fixed height** (like `300px`).  
  If the parent’s height is `auto` (meaning it grows with its content), then `50%` is meaningless → the browser ignores it.

**What trips people up:**  
You set `height: 100%` on a child, expecting it to fill the parent, but nothing happens.

**Fix:** Make sure the parent has an explicit height, or use `flexbox` / `grid` (they handle this differently).

---

## Big Rule #5: Margin collapsing – gaps disappear when boxes touch vertically

If you have two boxes stacked vertically:  
- Top box has `margin-bottom: 30px`
- Bottom box has `margin-top: 20px`

The gap between them is **not** 50px. It’s 30px (the larger one). The smaller margin collapses into the bigger one.

**What trips people up:**  
You expect 50px of space, you get 30px, and you think CSS is broken.

**Fix:** If you really need the sum, add a small border, padding, or use `display: flex` on the parent.

---

## Big Rule #6: `z-index` is not global – it’s local to each “stacking group”

You can put `z-index: 9999` on an element, but if its parent has `z-index: 1` (and also creates a stacking group), the child will *never* pop above something outside that parent.

**Simple version:**  
Think of stacking groups like separate decks of cards.  
You can move cards within your deck, but your whole deck might be under someone else’s deck.

**What trips people up:**  
You set a huge z-index but it still hides behind something else.

**Fix:** Check the parent chain. If any parent has `position`, `opacity less than 1`, or `transform`, it might be creating a new stacking group. Remove those or raise the parent’s z-index.

---

## Big Rule #7: `overflow: hidden` does two jobs

It hides content that spills out.  
**But also** it contains floating elements inside, and stops margins from collapsing through it.

**What trips people up:**  
You add `overflow: hidden` to “just hide overflow”, and suddenly your layout shifts in unexpected ways.

**Fix:** If you only want to hide overflow, you’re fine. But if your layout changes, now you know why.

---

## Big Rule #8: Inline elements ignore vertical spacing

`width`, `height`, `margin-top`, `margin-bottom` – inline elements ignore these.

**What trips people up:**  
You add `margin-top: 20px` to a `<span>` or `<a>` and nothing happens.

**Fix:** Use `display: inline-block` or `display: block` if you need vertical sizing or spacing.

---

## Your original rule (sizing vs alignment) is still one of the biggest

You already got that one. It applies especially in **flexbox** and **grid**:

- First: decide if the box should **stretch** (take all space) or **shrink** (fit content).
- Second: align the result (left, center, right, top, bottom).

Most beginners try to do both at once with one property. You saw through that.

---

**Takeaway:**  
Every time CSS surprises you, ask yourself:  
*“Am I trying to do two separate things with one simple rule?”*  
The answer is almost always yes.