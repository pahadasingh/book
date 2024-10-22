1. Centering Elements Vertically and Horizontally

---

Problem: Centering an element in a container both vertically and horizontally.

Solution: Use Flexbox.

```css
.container {
    display: flex;
    justify-content: center; /_ horizontal _/ 
    align-items: center; /_ vertical _/ 
    height: 100vh;
}
```

2. Responsive Text with `vw`

---

Problem: Ensuring text scales proportionally with the viewport.

Solution: Use `vw` units.

```css
h1 {
  font-size: 5vw;
}
```

3. Maintain Aspect Ratio

---

Problem: Maintaining aspect ratio for elements.

Solution: Use padding based on a percentage.

```css
.aspect-ratio-box {
    width: 100%;
    padding-top: 56.25%; /_ 16: 9 Aspect Ratio _/ 
    position: relative;
}

.aspect-ratio-content {
    position: absolute;
    top: 0;
    right: 0;
    bottom: 0;
    left: 0;
}
```

4. Custom Checkbox and Radio Buttons

---

Problem: Styling default checkboxes and radio buttons.

Solution: Hide the default input and style a label.

```html
<label class="custom-checkbox">
    <input type="checkbox"/>
    <span class="checkmark"></span> 
</label>

.custom-checkbox
  input {
  display: none;
}
.custom-checkbox .checkmark {
  width: 20px;
  height: 20px;
  background-color: #eee;
  border-radius: 4px;
}
.custom-checkbox input:checked + .checkmark {
  background-color: #2196f3;
}
```

5. CSS Grid for Layouts

---

Problem: Creating complex layouts.

Solution: Use CSS Grid.

```css
.container {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 10px;
}
.item {
  background-color: lightblue;
  padding: 20px;
}
```

6. Sticky Footer

---

Problem: Making a footer stick to the bottom of the page.

Solution: Use Flexbox.

```css
body {
  display: flex;
  flex-direction: column;
  min-height: 100vh;
}
main {
  flex: 1;
}
footer {
  background-color: #f1f1f1;
  padding: 10px;
  text-align: center;
}
```

7. Smooth Scroll

---

Problem: Adding smooth scroll to anchor links.

Solution: Use `scroll-behavior`.

```css
html {
  scroll-behavior: smooth;
}
```

8. Responsive Images

---

Problem: Ensuring images are responsive.

Solution: Use `max-width`.

```css
img {
  max-width: 100%;
  height: auto;
}
```

9. Text Truncation with Ellipsis

---

Problem: Truncating overflowing text.

Solution: Use `text-overflow`.

```css
.truncate {
    white-space: nowrap;
    overflow: hidden;
    text-overflow: ellipsis;
    width: 200px; /_ or any width _/
}
```

10. Custom Scrollbars

---

Problem: Styling scrollbars.

Solution: Use `::-webkit-scrollbar`.

```css
::-webkit-scrollbar {
  width: 10px;
}
::-webkit-scrollbar-track {
  background: #f1f1f1;
}
::-webkit-scrollbar-thumb {
  background: #888;
}
::-webkit-scrollbar-thumb:hover {
  background: #555;
}
```

11. Full-Screen Background Image

---

Problem: Making a background image cover the entire screen.

Solution: Use `background-size`.

```css
.full-screen-bg {
  background-image: url("background.jpg");
  background-size: cover;
  background-position: center;
  height: 100vh;
}
```

12. Animated Gradient Background

---

Problem: Creating an animated gradient background.

Solution: Use `@keyframes`.

```css
@keyframes gradient {
  0% {
    background-position: 0% 50%;
  }
  50% {
    background-position: 100% 50%;
  }
  100% {
    background-position: 0% 50%;
  }
}
.animated-gradient {
  background: linear-gradient(270deg, #ff7e5f, #feb47b);
  background-size: 400% 400%;
  animation: gradient 15s ease infinite;
}
```

13. Overlays

---

Problem: Adding an overlay to an image.

Solution: Use `::after` pseudo-element.

```css
.image-overlay {
    position: relative;
}

.image-overlay::after {
    content: '';
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background-color: rgba(0, 0, 0, 0.5); /_ black with 50% opacity _/
}
```

14. Image Hover Effects

---

Problem: Adding hover effects to images.

Solution: Use `:hover`.

```css
.image-hover img {
  transition: transform 0.3s;
}
.image-hover img:hover {
  transform: scale(1.1);
}
```

15. CSS Variables

---

Problem: Simplifying theme changes.

Solution: Use CSS variables.

```css
:root {
    --primary-color: #3498db;
    --secondary-color: #2ecc71;
}

button {
    background-color: var(--primary-color);
    color: var(--secondary-color);
}
```

16. Object Fit for Images

---

Problem: Ensuring images fit within their containers without distortion.

Solution: Use `object-fit`.

```css
.fit-image {
    width: 100%;
    height: 200px;
    object-fit: cover; /_ or contain, fill, etc. _/
}
```

17. Prevent Line Breaks

---

Problem: Preventing text from breaking into multiple lines.

Solution: Use `white-space`.

```css
.no-break {
  white-space: nowrap;
}
```

18. Full-Width Elements

---

Problem: Making an element span the full width of its parent.

Solution: Use `width: 100vw`.

```css
.full-width {
  width: 100vw;
  margin-left: calc(50% - 50vw);
  margin-right: calc(50% - 50vw);
}
```

19. SVG Icon Color Control

---

Problem: Changing the color of inline SVGs with CSS.

Solution: Use `currentColor`.

```css
.icon {
  fill: currentColor;
}
.icon-container {
  color: #ff6347;
}
```

20. CSS Grid with Named Areas

---

Problem: Creating complex layouts with named grid areas.

Solution: Use `grid-template-areas`.

```css
.grid-container {
  display: grid;
  grid-template-areas:
    "header header"
    "sidebar content"
    "footer footer";
  grid-gap: 10px;
}
.header {
  grid-area: header;
}
.sidebar {
  grid-area: sidebar;
}
.content {
  grid-area: content;
}
.footer {
  grid-area: footer;
}
```

21. CSS Transitions

---

Problem: Smoothly transitioning between states.

Solution: Use `transition`.

```css
.transition-button {
  background-color: #3498db;
  transition: background-color 0.3s;
}
.transition-button:hover {
  background-color: #2ecc71;
}
```

22. CSS Animations

---

Problem: Adding animations to elements.

Solution: Use `@keyframes`.

```css
@keyframes bounce {
  0%,
  100% {
    transform: translateY(0);
  }
  50% {
    transform: translateY(-20px);
  }
}
.bounce {
  animation: bounce 2s infinite;
}
```

23. CSS Shape Outsiders

---

Problem: Creating non-rectangular shapes.

Solution: Use `clip-path`.

```css
.clip-path {
  clip-path: polygon(50% 0%, 100% 50%, 50% 100%, 0% 50%);
  background-color: #3498db;
  width: 200px;
  height: 200px;
}
```

24. Dark Mode

---

Problem: Implementing dark mode.

Solution: Use CSS variables and media queries.

```css
:root {
    --bg-color: #fff;
    --text-color: #000;
}

@media (prefers-color-scheme: dark) {
    :root {
        --bg-color: #333;
        --text-color: #fff;
    }
}

body {
    background-color: var(--bg-color);
    color: var(--text-color);
}
```

25. CSS Counters

---

Problem: Creating a counter.

Solution: Use `counter-reset` and `counter-increment`.

```css
.counter-list {
  counter-reset: section;
}
.counter-list li::before {
  counter-increment: section;
  content: "Section " counter(section) ": ";
}
```

> These 25 CSS hacks can significantly improve your web development workflow, allowing you to solve common problems efficiently and create more responsive, dynamic web pages.
