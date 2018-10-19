# Disable Selection

- Makes content unselectable:

```html
<p>You can select me.</p>
<p class="unselectable">You can't select me!</p>
```

```css
.unselectable {
  user-select: none;
}
```

- Explanation:
    - `user-select: none` specifies that the class' text cannot be selected.
    - Really, it's only this :unamused:

> `user-select` actually can have quite a few other properties: `auto` (enables selection if the browser allows), `text` (enables text selection) and `all` (text selection is made with one click instead of a double-click. 