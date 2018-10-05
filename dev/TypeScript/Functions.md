# Functions

## Parameter annotations

- You can annotate function parameters as variables:
  ```ts
  let sample: { bar: number };
  function foo(sample: { bar: number }) {}
  ```

---

## Return type annotation

- You can annotate a function's return type just like the code below:

  ```ts
  interface Foo {
    foo: string;
  }

  // Return type annotated as `: Foo`
  function foo(sample: Foo): Foo {
    return sample;
  }
  ```

- But you actually **don't need** to do that since the return will be inferred by the compiler.
- Even thou, it's normally a good idea to annotate to help with errors and legibility.

---

## Optional parameters

- You can mark parameters as optional by the use of the `?` token:

  ```ts
  function foo(bar: number, bas?: string): void {
    // ..
  }

  foo(123);
  foo(123, 'hello');
  ```

- You can even provide a proper default value for parameters **even if they are not provided in the function call**:

  ```ts
  function foo(bar: number, bas: string = 'hello') {
    console.log(bar, bas);
  }

  foo(123); // 123, hello
  foo(123, 'world'); // 123, world
  ```

---

## Overloading

- TypeScript allows us to declare function overloads, as you can **make an unique implementation of several overloads**:
  ```ts
  function padding(all: number);
  function padding(topAndBottom: number, leftAndRight: number);
  function padding(top: number, right: number, bottom: number, left: number);
  // Actual implementation that is a true representation of all the cases the function body needs to handle
  function padding(a: number, b?: number, c?: number, d?: number) {
    if (b === undefined && c === undefined && d === undefined) {
      b = c = d = a;
    } else if (c === undefined && d === undefined) {
      c = a;
      d = b;
    }
    return {
      top: a,
      right: b,
      bottom: c,
      left: d
    };
  }
  ```
- Of course, you can create overloads with unique representation with no problem, as you'll probably do.
