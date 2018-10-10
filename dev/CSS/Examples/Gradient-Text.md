# Gradient Text

- Example to give some text a gradient color:

```css
.gradient-text {
  background: -webkit-linear-gradient(pink, red);
  -webkit-text-fill-color: transparent;
  -webkit-background-clip: text;
}
```

```html
<p class="gradient-text">Gradient text</p>
```

- Explanation:

  - `background: -webkit-linear-gradient(...)` gives the text element a gradient background
    - The first argument defines the starting gradient color (from the top of the element) and the second one, the ending gradient color (from the elements' bottom).
  - `-webkit-text-fill-color: transparent` specify the text color filling with transparent color.
  - `-webkit-background-clip: text` clips the background (that we already defined as a gradient) with the text element, filling all the text with the gradient backgrounf color.

- In other words, we:
  - Defined a `background` with our desired gradient color
  - Set the `text` color to transparent, as we are going to put some gradient flavor to it
  - Clipped the gradient background to the `text` element, effectively making our text awesome.
