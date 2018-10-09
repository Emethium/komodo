# rem vs em

- Both **rem** and **em** are metric units for typography.

- The thing is they are of equal value of the **current font-size**.

  - Which make them relative and commonly used as size units for responsive interfaces.

- So, `1em = 20px` if a selector has a `font-size` of `20px`.

- Even if it's possible you SHOULD NOT SET `font-size` in the `<html>` tag to a certain pixel value as it overrides the browser's settings.

  - You shoud really use a `percentage` value or simply not use the `font-size` declaration entirely.

- The funny part. Let's take a look in this piece of code:

  ```css
  h1 {
    font-size: 2em; /* 1em = 16px */
    margin-bottom: 1em; /* 1em = 32px */
  }

  p {
    font-size: 1em; /* 1em = 16px */
    margin-bottom: 1em; /* 1em = 16px */
  }
  ```

  - The entire point here is that **1em present different computed values** in each case
  - The `p` class seems to work as expected, uh?
  - But not the `h1`, yes?
    - Since `em` is equal to the `font-size`, when you define that `font-size: 2em;` **you override** the `em` default value.
    - So the **new** `em` metric becomes `2em`.
    - And then, when we define `margin-bottom: 1em;`, it'll actually have 32px, not 16px.

---

## What about REM?

- `rem` means **Root EM**, created to relieve us from the `em` computational problems.
- I guess you can imagine by now, but `1rem` **will be always equal** to the `font-size`.
- So, if we revisit our before facewd problem in a different approach:

  ```css
  h1 {
    font-size: 2rem;
    margin-bottom: 1rem; /* 1rem = 16px */
  }

  p {
    font-size: 1rem;
    margin-bottom: 1rem; /* 1rem = 16px */
  }
  ```

  - As you can see, that problem of "em value override" doesn't really apply here as `1rem` always have the same value .

---

## What should I use?

- `em` if the property scales according to it's `font-size`.
- `rem` in everything else.
