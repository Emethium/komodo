# Bouncing Loader

- Creates a boucing loader animation:

```css
@keyframes bouncing-loader {
  from {
    opacity: 1;
    transform: translateY(0);
  }
  to {
    opacity: 0.1;
    transform: translateY(-1rem);
  }
}
.bouncing-loader {
  display: flex;
  justify-content: center;
}
.bouncing-loader > div {
  width: 1rem;
  height: 1rem;
  margin: 3rem 0.2rem;
  background: #8385aa;
  border-radius: 50%;
  animation: bouncing-loader 0.6s infinite alternate;
}
.bouncing-loader > div:nth-child(2) {
  animation-delay: 0.2s;
}
.bouncing-loader > div:nth-child(3) {
  animation-delay: 0.4s;
}
```

```html
<div class="bouncing-loader">
  <div></div>
  <div></div>
  <div></div>
</div>
```

- Explanation:

  - The `@keyframes` tag defines an animation with two stages, as we can notice by the use of `from` and `to`.

    - The element is set to change the value `opacity` between transitions and also is translated up on the 2D plane by the use of `transform: translateY()`.
      - The `translateY()` argument is the length of the translation.

  - `bouncing-loader` is the parent container of the bouncing circles. We use the `display: flex` and `justify-content: center` to centralize it's children content.

  - `.bouncing-loader > div` targets the styling of the three child `div` of the parent `boucing-loader`.

    - Of course, any other `div` that we put inside the parent would also receive the styling we just set.
    - `margin: 3rem 0.2rem` defines the **top** and **bottom** margings, in this order.
    - `animation` is a shorthand property of:
      - `animation-name`: name for the @keyframes animation
      - `animation-duration`: defines the timeframe of each animation cycle
      - `animation-iteration-count`: defines the amount of animations iterations
      - `animation-direction`: with the `alternate` value, plays the animation forwards, then backwards

  - `nth-child(n)` is used to target the nth child element of a parent.

    - In our case `.bouncing-loader > div:nth-child(2)` is used to **target specifically the second `div` child of `bouncing-loader`**

  - It may be fairly obvious, but the `animation-delay` is used to give a delay to an element
    - Applied to our example, we gave different delays for each child so they **don't start at the same time**.
