Here are the other **big rules** of CSS layout — fundamental principles that explain how elements size, position, and interact with each other. Each is as counterintuitive as your two‑step sizing/alignment rule if you try to compress it into one step.

---

### 1. **Everything is a rectangle (the box model)**
Every element generates a box with **content → padding → border → margin**.  
- `width` / `height` alone only affect the *content* box (unless you change `box-sizing: border-box`).  
- The actual space an element takes up is `content + padding + border + margin`.  
- **One‑step thinking:** “I set width: 200px, so it’s 200px.”  
  **Two steps:** ① Calculate content width ② Add padding & border to get total width.

---

### 2. **Block vs Inline formatting context**
- **Block** elements: stretch to fill their container’s width (default = `width: auto` → take all available space).  
- **Inline** elements: shrink‑to‑fit their content width.  
- **One‑step thinking:** “This `<span>` should behave like a block.”  
  **Two steps:** ① Change `display: block` (sizing behavior) ② Now it stretches.

---

### 3. **The containing block – not always the parent**
Percentage values (`width: 50%`, `top: 20%`) and absolute positioning offsets are relative to the **nearest containing block**, which can be:  
- The parent (normal flow)  
- An ancestor with `position: relative/absolute/fixed/sticky`  
- The viewport (`position: fixed`)  
- A grid / flex container (special rules)  
- **One‑step thinking:** “`height: 100%` means parent’s height.”  
  **Two steps:** ① Find the actual containing block ② Compute the percentage relative to *its* property.

---

### 4. **Collapsing margins**
Adjacent vertical margins of block elements **overlap** (collapse) into a single margin equal to the larger of the two.  
- Parent + first/last child margins also collapse out of the parent.  
- **One‑step thinking:** “`margin-bottom: 20px` + `margin-top: 30px` = 50px gap.”  
  **Two steps:** ① Determine if margins are adjacent (no border, no padding, no formatting context) ② Use the max value.

---

### 5. **Positioning removes from flow (or not)**
- `static` / `relative`: element stays in normal flow, other elements respect its space.  
- `absolute` / `fixed`: element is **completely removed** from flow. Siblings ignore it. Its size defaults to shrink‑to‑fit unless you set a specific width.  
- **One‑step thinking:** “I’ll put an absolute menu and the footer will stay below it.”  
  **Two steps:** ① Remove element from flow ② The footer now moves up as if the menu never existed.

---

### 6. **Flexbox: main axis sizing + cross axis alignment**
Your original rule fits here perfectly. But there’s another:  
Flex items **stretch** on the cross axis by default.  
- **One‑step thinking:** “I want items aligned to the start, they should be as tall as their content.”  
  **Two steps:** ① Change cross‑axis sizing behavior: `align-self: start` (shrink‑to‑fit) ② Then align that result.

---

### 7. **Grid items stretch in both axes by default**
Unlike flex, CSS Grid items fill their entire grid area (cell) in **both dimensions** unless told otherwise.  
- `justify-self: stretch` (default) → item expands horizontally.  
- `align-self: stretch` (default) → item expands vertically.  
- **One‑step thinking:** “I set the item to align left, it will become width: auto.”  
  **Two steps:** ① Change stretching to shrink‑to‑fit (`justify-self: start`) ② Now position the shrunken item inside the cell.

---

### 8. **Percent heights need a defined parent height**
`height: 50%` only works if the parent has an **explicit height** (px, %, or absolute units). If parent is `height: auto`, the percentage is **undefined** → defaults to `auto`.  
- **One‑step thinking:** “Parent grows with content, child wants 50% of that.”  
  **Two steps:** ① Parent resolves `auto` height from content ② Child sees that `auto` has no numeric value → falls back to shrink‑to‑fit.

---

These rules, like yours, reveal that CSS almost never does two things in one step. Sizing and alignment are decoupled; flow and positioning are decoupled; collapsing margins require checking adjacency first. Once you see the **two‑step pattern**, most layout weirdness becomes predictable.