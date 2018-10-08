# Type Assertion

- TypeScript allows you to override the auto-inferred and analyzed types. It's basically saying **that you know better than the compiler does**.

- One common case is when we're porting code from JavaScript to TypeScript. Consider the following:
  ```ts
  var foo = {};
  foo.bar = 123; // Gives an error as 'bar' does not exist in {}
  foo.baz = 'hai'; // Also gives an error as 'baz' does not exist in {}
  ```
- One solution here lies in the definition of an `interface` and the `as` keyword:

  ```ts
  interface Foo {
    bar: number;
    baz: string;
  }

  var foo = {} as Foo;
  foo.bar = 123; // Ok!
  foo.baz = 'hai'; // Ok!
  ```

---

## `as foo` VS. `<foo>`

- Originally the syntax that was added was `<foo>`:

  ```ts
  var foo: any;
  var bar = <string>foo; // bar is now a string type
  ```

- However, that causes an grammar ambiguity when we're dealing with style assertions in JSX:

  ```ts
  var foo = <string>bar</string>;
  ```

- Therefore (even if you are not working with **React**) is reccomended that you just use `as foo` for consistency.

---

## Type Assertion vs. Casting

### Assertion considered harmful

- In many cases Type Assertion can be used as an useful tool to allow you to easly migrate from legacy code (a.k.a plain old JavaScript).
- But you must be careful, as the compiler will not **protect you from forgetting to add the properties you promised**.
  > The point here is to declare a new interface, add attributes, but forget to actually set them in code. Just not paying attention.
- Other bad scenario is when people use **assertion as a means of providing autocomplete**:

  ```ts
  interface Foo {
    foo: number;
    baz: string;
  }

  var foo <Foo> {
    // the compiler will provide autocomplete for properties of Foo
    // But it is easy for the developer to forget adding all the properties
    // Also this code is likely to break if Foo gets refactored (e.g. a new property added)
  }
  ```

  > And if you forget a property, the compiler won't even complain.

### Double Assertion

- The Type Assertion, despite being a bit unsafe, has very valid use cases. Just as:
  ```ts
  function handler(event: Event) {
    let mouseEvent = event as MouseEvent;
  }
  ```
- However, some situations are most likely errors and TypeScript will probably complain:
  ```ts
  function handler(event: Event) {
    let element = event as HTMLElement; // Error: Neither 'Event' nor type 'HTMLElement' is assignable to the other
  }
  ```
- But if you reeeeeeally want that type, you can use a double assertion by first asserting to `any`, which is compatible to all types:
  ```ts
  function handler(event: Event) {
    let element = (event as any) as HTMLElement; // Okay!
  }
  ```
  > It looks like a very bad idea to me, thou :hushed:
