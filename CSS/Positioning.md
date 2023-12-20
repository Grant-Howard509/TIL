# Positioning in CSS

We use the property `position` to set the element's position in the DOM. Some positions have other properties, `top`, `bottom`, `left`, and `right`, to help dictate where the element is placed.

## Positioning Types

### Static Positioning

Static positioning is the default for most DOM elements. The property offsets of `top`, `bottom`, `left`, and `right` have zero effect on the element's position in the DOM.

### Relative Positioning

Relative positioning uses the DOM element's default position in the normal flow but with an offset relative to the element itself. The offsets themselves do not affect the other neighboring elements position in the DOM. Although the element itself has repositioned, the space of the element as if it were static in the normal flow remains.

### Absolute Positioning

Elements that are absolute are completely removed from the normal flow within the DOM. The element is relative to either its closest ancestor or its containing block.

### Fixed Positioning

Similar to absolute, fixed positioning also removes the element out of the normal flow of the DOM. The fixed element is relative to its initial containing block.

### Sticky Positioning

Sticky elements are in the normal flow in the DOM but offset to its nearest scrolling ancestor or containing block. You can think of the sticky position as a combination between relative and fixed.

## Performance and Accessibility

- Make sure any elements set to absolute do not overlap other elements when the viewport increases or decreases.
- Note that the fixed and sticky positions can cause performance issues since the browser needs to repaint the element to its new location on the page.

As a last resort, set the fixed or sticky element with `will-change: transform;` if performance issues persist.
