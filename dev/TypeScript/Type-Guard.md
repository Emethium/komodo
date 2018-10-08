#Type Guard

- Type Guards allows you to narrow down the type of an object inside a conditional block.

## `typeof`

- TypeScript will be able to understand the different types of variables within some specific block.
- In the example below, TypeScript realizes that some function does not actually exists and points out it's probably a typo:
  ```ts
  function doSomething(x: number | string) {
    if (typeof x === 'string') {
      // Within the block TypeScript knows that `x` must be a string
      console.log(x.subtr(1)); // Error, 'subtr' does not exist on `string`
      console.log(x.substr(1)); // OK
    }
    x.substr(1); // Error: There is no guarantee that `x` is a `string`
  }
  ```

---

## `instanceof`

- I believe it's really straightforward:

  ```ts
  class Foo {
    foo = 123;
    common = '123';
  }

  class Bar {
    bar = 123;
    common = '123';
  }

  function doStuff(arg: Foo | Bar) {
    if (arg instanceof Foo) {
      console.log(arg.foo); // OK
      console.log(arg.bar); // Error!
    }
    if (arg instanceof Bar) {
      console.log(arg.foo); // Error!
      console.log(arg.bar); // OK
    }

    console.log(arg.common); // OK
    console.log(arg.foo); // Error!
    console.log(arg.bar); // Error!
  }

  doStuff(new Foo());
  doStuff(new Bar());
  ```

---

## `in`

- It allows a **safe checking** for the existance of a property in an object:

  ```ts
  interface A {
    x: number;
  }
  interface B {
    y: string;
  }

  function doStuff(q: A | B) {
    if ('x' in q) {
      // q: A
    } else {
      // q: B
    }
  }
  ```

---

## Literal Type Guard

- When you have **literal types** (a.k.a `type`) you can check them to discriminate:

  ```ts
  type Foo = {
    kind: 'foo'; // Literal type
    foo: number;
  };
  type Bar = {
    kind: 'bar'; // Literal type
    bar: number;
  };

  function doStuff(arg: Foo | Bar) {
    if (arg.kind === 'foo') {
      console.log(arg.foo); // OK
      console.log(arg.bar); // Error!
    } else {
      // MUST BE Bar!
      console.log(arg.foo); // Error!
      console.log(arg.bar); // OK
    }
  }
  ```
