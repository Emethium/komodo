# Functional Programming in JavaScript

## Pure functions

- What defines a **pure function**?

  - It always returns the same result if given the same arguments (also called _deterministic_)
  - It does not cause any observable side effects

- **It always returns the same result if given the same arguments**

  - Imagine we want to implement a function that calculates the area of a circle:

  ```js
  const PI = 3.14;

  function calculateArea(radius) {
    return radius * radius * PI;
  }

  calculateArea(10); // returns 314.0
  ```

  - But this is **not a pure function**. And why is that?

    - Since it **used a global object** that was **not passed as a parameter** to the function, it **cannot be called pure**.
    - So if we change the global `PI` value to `42`, for example, that would result in `4200`. We would have got a different result with the same parameters! (`radius` = 10)

  - But we can easily fix that:

  ```js
  const PI = 3.14;

  function calculateArea(radius, pi) {
    return radius * radius * pi;
  }

  calculateArea(10, PI); // returns 314.0
  ```

  - Since we always pass the `PI` value as a parameters, all the parameters are feed to the function without external object interference. **Now we can say we have a pure function**.

- **Reading files**

  - If our function reads external files, it cannot be a pure function **as the file's contents can change**.

- **Random number generation**

  - Any function that **relies** on random number generation cannot be pure.

- **It does not cause any observable side effects**

  - Examples of "Observable side effects" include: modifying a global object or a parameter passed by reference.
  - If we implement a function to recieve an integer value and return the value increased by 1:

  ```js
  let counter = 1;

  function increaseCounter(value) {
    counter = value + 1;
  }

  increaseCounter(counter);
  console.log(counter); // 2
  ```

  - The issue here is that our impure function recieves the value but re-assigns the outerly scoped `counter` with it's value increased by one. In other words, we modified a global object so our function **cannot be called pure**.
  - Transforming our function into a pure one is a very simple task, tho:

  ```js
  let counter = 1;

  function increaseCounter(value) {
    return value + 1;
  }

  increaseCounter(counter); // 2
  console.log(counter); // 1
  ```

  - Now our **function is pure**. We do not change the global scoped variable anymore, just returning the increment of it's value.

- **Pure functions benefits**
  - Functions are isolated and are unable to impact in other parts of our system
  - Given the same parameters, pure functions always return the same value
  - We don't need to think of situations when the same parameters have different results **as they will never happen**
  - Easier to test code
