# Donut Spinner

- Creates a donut spinner to normally point some content's loading:

```html
<div class="donut"></div>
```

```css
@keyframes donut-spin {
  0% {
    transform: rotate(0deg);
  }
  100% {
    transform: rotate(360deg);
  }
}
.donut {
  display: inline-block;
  border: 4px solid rgba(0, 0, 0, 0.1);
  border-left-color: #7983ff;
  border-radius: 50%;
  width: 30px;
  height: 30px;
  animation: donut-spin 1.2s linear infinite;
}
```

- Explanation:
  - As the `@keyframes` represents a multi-stage animation, we defined two **selectors**: `0%` and `100%`.
    - The first one (0%) defines the attributes at the beginning of the animation, and the last one (100%) defines the attributes at the end of the animation.
    - This `0%` to `100%` structure is equivalent to the `from` and `to` one you **may have read** in another file in this repository or not.
