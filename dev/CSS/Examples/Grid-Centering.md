# Grid Centering

- Showing how to center an child element both vertically and horizontally:

```css
.grid-centering {
  display: grid;
  justify-content: center;
  align-items: center;
  height: 100px;
}
```

```html
<div class="grid-centering">
  <div class="child">Centered content.</div>
</div>
```

- Explanation:
  - `display: grid` sets an HTML element as a grid container.
  - `justify-content: center` aligns the container's items on the main axis horizontally.
  - `align-items: center` is used to specify the default alignment for items inside the container.
  - `height: 100px` is self-explanatory.
