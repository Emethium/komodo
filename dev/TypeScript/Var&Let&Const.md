# Var, Let and Const

## Var

- First of all, we shouldn't use `var` anymore.
- `var` variables in JavaScript (and TypeScript, by extension) are **function scoped**, not **block scoped** as most languages.

  - Which means that when we use `{}`, we **do not create a new variable scope**.
  - Which also means that a variable is the same **inside** and **outside** the brackets.
  - As an example, you may expect the following to print `123`, but instead it'll print `456`:

    ```ts
    var foo = 123;
    if (true) {
      var foo = 456;
    }

    console.log(foo); // 456
    ```

  - But the expected value would be achieved using a function, as we have mentioned that `var` variables are function scoped:

    ```ts
    var foo = 123;
    function test() {
      var foo = 456;
    }
    test();
    console.log(foo); // 123
    ```

- Those mentioned are common errors and that's exactly why **ES6** brought us the `let` and `const` keywords so we can define a true block scope.
- As such, **do not** use `var`.

---

## Let

- Using `let` we get a true unique element disconected from what we may have defined outside a scope. Rewriting our last example with `let`:

  ```ts
  let foo = 123;
  if (true) {
    let foo = 456;
  }
  console.log(foo); // 123
  ```

- The same idea would happen to save you if you happen to use the same variable name for a `for` loop iterable and such.
- It's also possible to wrap `case` bodies in `{}` to reuse variable names, as shown below:
  ```ts
  switch (name) {
    case 'x': {
      let x = 5;
      // ...
      break;
    }
    case 'y': {
      let x = 10;
      // ...
      break;
    }
  }
  ```
- The `let` and `const` (which will be discussed just below) keywords have several behaviour in common. But the main difference in use that we must already state is that: `let` keyward will be used for mutable objects and the `const` keyword for objects that shouldn't be mutable.

---

## Const

- `let` counterpart used for immutable variables, just as I told you.
- It's considered a good practice always start using `const` for **all** your variables and then changing them do `let` if they'll be mutated.
- It's also a good practice to use `const` variables for readability and maintainability, as:

  ```ts
  // Low readability
  if (x > 10) {
  }

  // Better!
  const maxRows = 10;
  if (x > maxRows) {
  }
  ```

- A `const` declaration **must** be initialized. Otherwise we get another kind compilation error:
  ```ts
  const foo; // ERROR: const declarations must be initialized
  ```
- A `const` declaration **must not** be reassigned. Well, since we already discussed that a `const` variable is a imutable and constant object, we obviously will get a compilation error:
  ```ts
  const foo = 123;
  foo = 456; // ERROR: Left-hand side of an assignment expression cannot be a constant
  ```
- It also works with object literals, protecting the **variable reference**:
  ```ts
  const foo = { bar: 123 };
  foo = { bar: 456 }; // ERROR : Left hand side of an assignment expression cannot be a constant
  ```
  - But it **only protects the reference**, object properties can **still be mutated**:
  ```ts
  const foo = { bar: 123 };
  foo.bar = 456; // Allowed!
  console.log(foo); // { bar: 456 }
  ```
