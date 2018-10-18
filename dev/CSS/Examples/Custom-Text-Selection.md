# Custom Text Selection

- Changes the styling of a text selection:

```html
<p class="custom-text-selection">Select some of this text.</p>
```

```css
::selection {
  background: aquamarine;
  color: black;
}
.custom-text-selection::selection {
  background: deeppink;
  color: white;
}
```

- Explanation
  - `::selection` defines a pseudo selector on text content for any element, when selected.
    - If `::selected` is defined, but not combined to any CSS element, it'll be auto-applied for the **entire document** at **root level**.
    - Only a few CSS can be used with this selector: **color, background, cursor, and outline**.
  
  - `.custom-text-selection` is used ot define the styling of the selection outline. As we can see, the `::selection` was applied after the CSS class declaraton.
    - `background` will set the background color of the **selection**, so a deep pink one should appear if we select the text.
    - `color` will set the color of the font for the text, **when selected**.
  

> It's worth mentioning that we applied the `::selection` behaviour to the `custom-text-selection` class, but we didn't inherit the `aquamarine` and `black` colors because we **overwrote both properties in the custom class**. So, if we were to erase the two properties from the `custom-text-selection` class, our color behaviour would be just as we defined in `::selection`. It kinda works as interface implementation method override :information_desk_person:

