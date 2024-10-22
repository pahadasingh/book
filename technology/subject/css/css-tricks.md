Let's go!

### 01. Smooth scrolling on your website

Add scroll-behavior: smooth to the <html> element to enable smooth scrolling for the whole page.

```css
html{
    scroll-behavior: smooth;
  }
```

### 02. attribute selector for links

This selector targets links with href attributes starting with „https."

```css
a[href^="https"]{
    color: blue;
  }
```

### 03. ~ for combining siblings

Selects all <p> elements that are siblings following an <h2>.

```css
h2 ~ p{
    color: blue;
  }
```

### 04. the :not() pseudo class

This selector applies styles to list items that do not have the class „special."

```css
li:not(.special){
        font-stlye: italic;
    }
```

### 05. Viewport units for responsive typography

Using viewport units (vw, vh, vmin, vmax) can make font sizes responsive to the viewport size.

```css
h1{
    font-size: 5vw;
  }
```

### 06. :empty for empty elements

This selector targets empty <p> elements and hides them.

```css
p:empty{
    display: none;
  }
```

### 07. Custom properties (variables)

You can define and use custom properties for easier theming and maintenance.

```css
:root{
    --main-color: #3498db;
  }

  h1{
    color: var(--main-color);
  }
```

### 08. Object-fit property for image control

object-fit controls how the content of replaced elements (like <img>) should be resized.

```css
img{
    width: 100px;
    height: 100px;
    object-fit: cover;
  }
```

### 09. Grid for simplified layouts

CSS Grid provides a powerful way to create layouts in a more straightforward manner.

```css
.container{
    display: grid;
    grid-tempalte-columns: 1fr 2fr 1fr;
 }
```

### 10. :focus-within pseudo class

The :focus-within selects an element if that element contains any children that have :focus.

```css
form:focus-within{
    box-shadow: 0 0 5px rgba(0, 0, 0, 0, 0.2);
 }
```

### 11. Vertical centering with flexbox

Easily center content both horizontally and vertically within a container using flexbox.

```css
.container {
   display: flex;
   align-items: center;
   justify-content: center;
}
```

### 12. Custom highlight color for selections

Customize the highlight color when text is selected on your webpage.

```css
::selection {
   background-color: #ffcc00;
   color: #333;
}
```

### 13. Styling placeholder text

Style the placeholder text inside input fields.

```css
::placeholder {
   color: #999;
   font-style: italic;
}
```

### 14. Gradient borders

Create gradient borders using the *background-clip* property.

```css
.element {
   border: 2px solid transparent;
   background-clip: padding-box;
   background-image: linear-gradient(to right, red, blue);
}
```

### 15. Variable font sizes with vw

Adjust font size based on the viewport width, allowing for more responsive typography.

```css
body {
   font-size: calc(16px + 1vw);
}
```

### 16. Conic gradients for colorful elements

Create colorful and dynamic backgrounds using conic gradients.

```css
.element {
   background: conic-gradient(#ff5733, #33ff57, #5733ff);
}
```

### 17. Clamp() function for responsive text

Use the *clamp()* function to set a range for font size, ensuring readability on different screen sizes.

```css
.text {
   font-size: clamp(16px, 4vw, 24px);
}
```

### 18. Efficient font loading with font display swap

Use the *font-display: swap;* property to improve the performance of web fonts by displaying fallback fonts while the custom font is loading.

```css
@font-face {
   font-family: 'YourFont';
   src: url('your-font.woff2') format('woff2');
   font-display: swap;
}
```

### 19. Custom scroll snap points

Implement custom scroll snap points for a smoother scrolling experience, especially useful for image galleries or sliders.

```css
.scroll-container {
   scroll-snap-type: y mandatory;
}

.scroll-item {
   scroll-snap-align: start;
}
```

### 20. Variable font styling with font variation settings

Utilize variable fonts and the *font-variation-settings* property for fine-tuned control over font weight, style, and other variations.

```css
.text {
   font-family: 'YourVariableFont', sans-serif;
   font-variation-settings: 'wght' 500, 'ital' 1;
}
```

### 21. Custom underlines

Customize the style of underlines on links using a combination of border-bottom and text-decoration.

```css
a {
    text-decoration: none;
    border-bottom: 1px solid #3498db;
}
```

### 22. Hidden accessibility text

Use the class sr-only to visually hide elements but keep them accessible to screen readers.

```css
.sr-only {
    position: absolute;
    width: 1px;
    height: 1px;
    margin: -1px;
    padding: 0;
    overflow: hidden;
    clip: rect(0, 0, 0, 0);
    border: 0;
}
```

### 23. Aspect ratio boxes

Maintain aspect ratio for elements like images or videos by using the padding trick.

```css
.aspect-ratio-box {
    position: relative;
    width: 100%;
    padding-bottom: 75%; /* Adjust as needed */
}

.aspect-ratio-box > iframe {
    position: absolute;
    width: 100%;
    height: 100%;
}
```

### 24. Selecting even and odd elements

Style alternate elements using the :nth-child pseudo-class.

```css
li:nth-child(even) {
    background-color: #f2f2f2;
}

li:nth-child(odd) {
    background-color: #e6e6e6;
}
```

### 25. CSS Counter

Use the counter-reset and counter-increment properties to create automatic numbering in lists.

```css
ol {
    counter-reset: item;
}

li {
    counter-increment: item;
}
li::before {
    content: counter(item) ". ";
}
```

### 26. Multiple background images

Apply multiple background images to an element with different properties.

```css
.bg {
    background-image: url('image1.jpg'), url('image2.jpg');
    background-position: top left, bottom right;
    background-repeat: no-repeat, repeat-x;
}
```

### 27. Hyphens for better text flow

Improve text readability by allowing automatic hyphenation using the hyphens property.

```css
p {
    hyphens: auto;
}
```

### 28. CSS variables for dynamic styling

Leverage CSS variables to create dynamic and reusable styles.

```css
:root {
    --main-color: #3498db;
}

.element {
    color: var(--main-color);
}
```

### 29. Focus styles for keyboard navigation

Improve focus styles for better keyboard navigation and accessibility.

```css
:focus {
    outline: 2px solid #27ae60;
}
```

### 30. Smooth gradient transitions

Apply smooth transitions to gradient backgrounds for a polished effect.

```css
.gradient-box {
    background: linear-gradient(45deg, #3498db, #2ecc71);
    transition: background 0.5s ease;
}

.gradient-box:hover {
    background: linear-gradient(45deg, #e74c3c, #f39c12);
}
```

### 31. Text stroke effect

Add a stroke (outline) to your text for a unique visual effect.

```css
h1 {
    color: #3498db;
    -webkit-text-stroke: 2px #2c3e50;
}
```

### 32. CSS only hamburger menu

Create a simple hamburger menu without JavaScript.

```css
.menu-toggle {
    display: none;
}

.menu-toggle:checked + nav {
    display: block;
}
/* Add styles for the hamburger icon and menu here */
```

### 33. CSS :is() selector

Simplify complex selectors using the :is() pseudo-class.

```css
:is(h1, h2, h3) {
    color: blue;
}
```

### 34. Calculation in CSS variables

Perform calculations within CSS variables for dynamic styles.

```css
:root {
    --base-size: 16px;
    --header-size: calc(var(--base-size) * 2);
}

h1 {
    font-size: var(--header-size);
}
```

### 35. attr() function for content

Use the attr() function to retrieve and display attribute values.

```css
div::before {
    content: attr(data-custom-content);
}
```

### 36. CSS masking

Apply masking to images for creative effects.

```css
.masked-image {
    mask: url(mask.svg);
    mask-size: cover;
}
```

### 37. Blend modes

Experiment with blend modes for interesting color effects.

```css
.blend-mode {
    background: url(image.jpg);
    mix-blend-mode: screen;
}
```

### 38. aspect-ratio property

Simplify the creation of aspect ratio boxes with the aspect-ratio property.

```css
.aspect-ratio-box {
    aspect-ratio: 16/9;
}
```

### 39. shape-outside for text wrapping

Use the shape-outside property to make text wrap around a specified shape, allowing for more dynamic layouts.

```css
.shape-wrap {
    float: left;
    width: 150px;
    height: 150px;
    shape-outside: circle(50%);
}
```

### 40. ch unit for consistent sizing

The ch unit represents the width of the character "0" in the chosen font. It's useful for creating consistent and responsive layouts.

```css
h1 {
    font-size: 2ch;
}
```

### 41. ::marker pseudo-element

Style list item markers using the ::marker pseudo-element.

```css
li::marker {
    color: blue;
}
```

### 42. element() function for backgrounds

Dynamically reference an element as a background with the element() function.

```css
.background {
    background: element(#targetElement);
}
```

### 43. Sticky footers with Flexbox

Create a sticky footer layout using Flexbox.

```css
body {
    display: flex;
    flex-direction: column;
    min-height: 100vh;
}
main {
    flex: 1;
}
```

### 44. scroll-padding for smooth scrolling

Improve scrolling behavior by adjusting the scroll padding.

```css
html {
    scroll-padding: 20px;
}
```

### 45. Interactive highlight effect

Create an interactive highlight effect with CSS variables.

```css
.highlight {
    --highlight-color: #e74c3c;
    background-image: linear-gradient(transparent 0%, var(--highlight-color) 0%);
    background-size: 100% 200%;
    transition: background-position 0.3s;
}

.highlight:hover {
    background-position: 0 100%;
}
```

### 46. Custom radio buttons and checkboxes

Style radio buttons and checkboxes without images.

```css
input[type="radio"] {
    appearance: none;
    -webkit-appearance: none;
    border-radius: 50%;
    width: 16px;
    height: 16px;
    border: 2px solid #3498db;
}

input[type="checkbox"] {
    appearance: none;
    -webkit-appearance: none;
    width: 16px;
    height: 16px;
    border: 2px solid #e74c3c;
}
```

### 47. resize property for textarea

Control the resizing behavior of textareas using the resize property.

```css
textarea {
    resize: vertical;
}
```

### 48. Text gradient

Create a gradient effect for text using the background-clip and text-fill-color properties.

```css
.gradient-text {
    background-image: linear-gradient(45deg, #3498db, #2ecc71);
    background-clip: text;
    color: transparent;
}
```

### 49. word-break property for long words

Use the word-break property to control how long words or strings without spaces should be broken and wrapped.

```css
.long-words {
    word-break: break-all;
}
```

### 50. font-variation-settings for variable fonts

Fine-tune variable font styles using the font-variation-settings property.

```css
.custom-font {
    font-family: 'MyVariableFont';
    font-variation-settings: 'wght' 600, 'ital' 1;
}
```

### 51. Mix-blend-mode for creative overlays

Use mix-blend-mode to apply blending modes to elements, creating interesting visual effects when overlaying elements.

```css
.overlay {
  mix-blend-mode: overlay;
}
```

### 52. Styling broken images

Apply styles to broken images using the :broken pseudo-class.

```css
img:broken {
  filter: grayscale(100%);
}
```

### 53. CSS shapes

Use CSS shapes to create interesting designs using the shape-outside property.

```css
.shape {
  shape-outside: circle(50%);
}
```

### 54. Attribute selectors for substring matching

Use attribute selectors with the *= operator for substring matching.

```css
[data-attribute*="value"] {
  /* Styles */
}
```

### 55. Backdrop-filter for blurred backgrounds

Apply a blur effect to the background using backdrop-filter for a frosted glass effect.

```css
.element {
  backdrop-filter: blur(10px);
}
```

### 56. CSS environment variables

Access environment variables in CSS using the env() function.

```css
.element {
  margin-top: env(safe-area-inset-top);
}
```

### 57. CSS attribute counters

Count occurrences of a specific attribute value using the :nth-child selector.

```css
[data-category="example"]:nth-child(3) {
  /* Styles for the third occurrence */
}
```

### 58. CSS shapes for text wrapping

Use shape-outside with the polygon() function for precise text wrapping around irregular shapes.

```css
.text-wrap {
  shape-outside: polygon(0 0, 100% 0, 100% 100%);
}
```

### 59. Custom cursor styles

Change the cursor style using the cursor property.

```css
.custom-cursor {
  cursor: pointer;
}
```

### 60. HSLA for transparent colors

Use HSLA values for transparent colors, providing more control over the alpha channel.

```css
.transparent-bg {
  background-color: hsla(120, 100%, 50%, 0.5);
}
```

### 61. text-orientation for vertical text

Rotate text vertically using the text-orientation property.

```css
.vertical-text {
  text-orientation: upright;
}
```

### 62. font-variant for small caps

Apply small caps to text using the font-variant property.

```css
.small-caps {
  font-variant: small-caps;
}
```

### 63. box-decoration-break for background split

Control the background of an element that breaks across multiple lines using box-decoration-break.

```css
.split-background {
  box-decoration-break: clone;
}
```

### 64. :focus-visible for specific focus styling

Apply styles only when an element is in focus and the focus is not provided by a mouse click.

```css
input:focus-visible {
  outline: 2px solid blue;
}
```

### 65. text-rendering for optimal font rendering

Improve text rendering with the text-rendering property.

```css
.optimized-text {
  text-rendering: optimizeLegibility;
}
```

### 66. initial-letter for drop caps

Style the first letter of a block-level element with initial-letter.

```css
p::first-letter {
  font-size: 2em;
}
```

### 67. overscroll-behavior for scroll overshooting

Control the behavior when users scroll past the boundaries of a scroll container.

```css
.scroll-container {
  overscroll-behavior: contain;
}
```

### 68. writing-mode for vertical layout

Create a vertical layout using the writing-mode property.

```css
.vertical-layout {
  writing-mode: vertical-rl;
}
```

### 69. ::cue for styling HTML5 captions

Style HTML5 caption text using the ::cue pseudo-element.

```css
::cue {
  color: blue;
}
```

### 70. line-clamp for truncated multiline text

Limit the number of lines shown within an element with the line-clamp property.

```css
.truncated-text {
  display: -webkit-box;
  -webkit-line-clamp: 3;
  -webkit-box-orient: vertical;
  overflow: hidden;
}
```

### 71. scroll-snap-align

The scroll-snap-align property controls the alignment of scroll snap points within a scrolling container, ensuring precise control over scrolling behavior and enhancing user experience.

```css
.container {
  scroll-snap-type: x mandatory;
}
.item {
  scroll-snap-align: center;
}
```

### 72. overscroll-behavior

overscroll-behavior enables you to define how browsers should handle scroll overshooting, preventing unwanted scrolling effects and improving the overall scrolling experience.

```css
.scrollable {
  overscroll-behavior: contain;
}
```

### 73. font-kerning

font-kerning allows for fine-tuning of character spacing, ensuring optimal readability by adjusting the spacing between characters within text elements.

```css
p {
  font-kerning: auto;
}
```

### 74. shape-margin

When used in conjunction with CSS shapes, shape-margin specifies the margin around a floated element's shape, enabling refined control over text wrapping and layout.

```css
.shape {
  shape-margin: 20px;
}
```

### 75. scroll-margin

scroll-margin sets the margin between the edge of a scrolling container and the start of scrolling content, enhancing user experience by providing buffer space for scrolling.

```css
.container {
  scroll-margin-top: 100px;
}
```

### 76. tab-size

scroll-margin sets the margin between the edge of a scrolling container and the start of scrolling content, enhancing user experience by providing buffer space for scrolling.

```css
pre {
  tab-size: 4;
}
```

### 77. text-align-last

text-align-last determines the alignment of the last line of text within a block element, offering precise control over text alignment in multi-line blocks.

```css
p {
  text-align-last: justify;
}
```

### 78. text-justify

This property controls text justification behavior, specifying whether inter-word or inter-character spacing should be used for text justification.

```css
p {
  text-align: justify;
  text-justify: inter-word;
}
```

### 79. column-fill

column-fill dictates how content is distributed across multi-column layouts, allowing for sequential or balanced distribution of content across columns.

```css
.container {
  column-count: 3;
  column-fill: auto;
}
```

### 80. outline-offset

The outline-offset adjusts the space between an outline and the edge of an element, enabling finer control over the appearance of outlines without affecting layout.

```css
button {
  outline: 2px solid blue;
  outline-offset: 4px;
}
```

### 81. font-variant-numeric

This property allows for fine-grained control over numeric typographic rendering, enabling features such as lining and old-style numerals, fractions, and ordinal indicators.

```css
p {
  font-variant-numeric: lining-nums;
}
```

### 82. font-optical-sizing

Enable or disable font optical sizing to adjust the spacing and proportions of characters for improved visual harmony at various font sizes.

```css
p {
  font-optical-sizing: auto;
}
```

### 83. text-decoration-thickness

Control the thickness of text decorations such as underlines, overlines, and line-throughs for precise customization.

```css
p {
  text-decoration-thickness: 2px;
}
```

### 84. text-underline-offset

Adjust the position of underlines relative to the baseline of text for improved typographic refinement.

```css
p {
  text-underline-offset: 3px;
}
```

### 85. scroll-padding-block

Define padding space added around scrollable block containers to ensure content remains visible and accessible during scrolling.

```css
.container {
  scroll-padding-block: 20px;
}
```

### 86. scroll-padding-inline

Set padding space added around scrollable inline containers to enhance user experience during scrolling interactions.

```css
.container {
  scroll-padding-inline: 10px;
}
```

### 87. line-break

Specify how lines are broken within words or characters to control line wrapping behavior for improved text layout and readability.

```css
p {
  line-break: strict;
}
```

### 88. box-decoration-break

Control the rendering of border and padding across fragmented elements to ensure consistent styling of elements that are split across multiple lines or columns.

```css
.element {
  box-decoration-break: clone;
}
```

### 89. initial-letter

Style the first letter or initial character of a block element for decorative drop caps or other visually prominent initial characters.

```css
p::first-letter {
  font-size: 2em;
  float: left;
}
```

### 90. image-rendering

Adjust the rendering quality and performance of images to optimize image display for various scenarios.

```css
img {
  image-rendering: pixelated;
}
```

### 91. font-feature-settings

font-feature-settings allows you to enable or disable OpenType features in fonts, such as ligatures, kerning, and stylistic alternates.

```css
p {
  font-feature-settings: "liga" on;
}
```

### 92. text-orientation

This property controls the orientation of text within its containing box, enabling vertical or sideways text layout.

```css
.vertical-text {
  text-orientation: sideways;
}
```

### 93. text-decoration-skip-ink

text-decoration-skip-ink controls whether text decorations should skip over ascenders and descenders, improving the appearance of underlines and line-throughs.

```css
p {
  text-decoration-skip-ink: auto;
}
```

### 94. text-underline-position

text-underline-position adjusts the position of underlines relative to the text baseline, allowing for precise control over underline placement.

```css
p {
  text-underline-position: under;
}
```

### 95. image-orientation

image-orientation controls the orientation of an image, allowing you to rotate or flip it as needed.

```css
img {
  image-orientation: from-image;
}
```

### 96. column-span

column-span allows an element to span multiple columns in a multi-column layout, enabling more flexible and dynamic designs.

```css
.spanning-element {
  column-span: all;
}
```

### 97. contain

contain specifies a containment policy for an element, enabling optimizations by limiting the scope of layout calculations and rendering, which can improve performance.

```css
.optimized-element {
  contain: layout;
}
```

### 98. content-visibility

content-visibility allows you to control the rendering behavior of off-screen or hidden content, improving rendering performance by skipping the layout and painting phases for hidden elements.

```css
.off-screen {
  content-visibility: auto;
}
```

### 99. text-decoration-style

text-decoration-style specifies the style of the line used for text decoration, allowing you to choose between different line styles such as solid, double, dotted, or dashed.

```css
p {
  text-decoration: underline;
  text-decoration-style: wavy;
}
```

### 100. word-spacing

word-spacing adjusts the spacing between words in text elements, allowing you to fine-tune typographic layout and improve readability.

```css
p {
  word-spacing: 2px;
}
```