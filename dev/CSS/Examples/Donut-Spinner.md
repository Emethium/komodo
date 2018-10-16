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
    - This `0%` to `100%` structure is equivalent to the `from` and `to` one you **may have read** in another file in this repository, or not.
    - The `transform` property is used to apply a 2D or 3D transformation to an element. By doing so, we can rotate, move, scale, etc. elements.
    - `rotate` here, as the name may suggest, is a function that defines a transformation to rotate an element in an fixed point of the 2D plane. It receives an angle as argument.
      - With this effect we can actually make our donut spin. But, of course, we need to change something in the donut styling so we **can actually see** something rotating.

  - As for the donut's styling:

    - `display` is use to define what kind of box is generated for the element. We can mostly see `inline`,`block` or `inline-block` box formats:

      - `inline`: boxes are rendered in a line without causing it to break. These kinds of elements can have `padding` and `margin`, but cannot have `width` and `height`.
      - `block`: boxes are rendered in a new line, serving mostly as containers for other elements.
      - `inline-block`: boxes are rendered in as inline elements, but can have altered `width` and `heigth` values (differently from pure `inline` elements). **That's what we used here**.

    - `border` is a shorthand property used to define, **in this order**: width, border style and color of the top, right, bottom and left border of a box.

      - So we set a value of `4px` for the box `border`, as we can see.
      - Our second argument sets our border styling. There are several possible values here, but the `solid` one that we used defines a border as a **straigth line**.
      - The last argument is our border color, which is something like gray.

    - `border-left-color` is used to set the color of the left border of the element, a blue-ish thing in this case. That's the different shenanigan that will actually show the rotating animation effect.

    - `border-radius` is a shorthand property used to round the corners of an element. The **percentage** value here is used to create a fully circular (or elliptical) shape, `50%` defining a perfect circle with the same `heigth` and `width`.

    - The `animation` is a shorthand property several possible properties:
      - Our first one is `animation-name`, the name for the @keyframes animation
      - The second is `animation-duration`: defining the timeframe of each animation cycle
      - The third one is `animation-timing-function`, that sets the speed curve of the animation with the same speed, beginning to end
      - And finally the `animation-iteration-count` that defines the amount of animation iterations. In our case, as being `infinite`.
