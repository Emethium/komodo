# Etched text

- Creates an effect where text appears to be engraved into the background:

```html
<p class="etched-text">I appear etched into the background.</p>
```

```css
.etched-text {
  text-shadow: 0 2px white;
  font-size: 1.5rem;
  font-weight: bold;
  color: #b8bec5;
}
```

- Explanation:
    - The `text-shadow` property is used to add shadow to the text.
        - The arguments are used to create a white shadow offset, `0px` horizontally and `2px` vertically from the origin position.
    - The **background should be darker than the shadow** in order for the effect to work.
    - The text color should be slightly faded to make it look like it's been engraved out of the background.
    - From what I can observe we'll mostly use the `text-shadow` property with the first argument as the same `0px`, otherwise the shadow will look weird and deslocated :sweat: