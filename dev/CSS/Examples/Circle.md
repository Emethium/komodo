# Circle

- We're drawing a circle of pure CSS:

```css
.circle {
  border-radius: 50%;
  width: 2rem;
  height: 2rem;
  background: #333;
}
```

```html
<div class="circle"></div>
```

- Explanation:
  - `border-radius` is a property used to round the corners of an element.
    - The **percentage** used here means that the property will be set to `50%` of the class' parent property value.
  - `width` and `height` are self-explanatory properties.
    - Changing this values would cause alteration in the class roundness, creating an ellipse.
  - The `background: #333;` property will fill the `circle` element background with a blackish color. We're talking about the **background inside the drawin circle**, so the rendered element will be a simple black circle.
