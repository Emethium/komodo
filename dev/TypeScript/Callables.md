# Callables

- Callables can be annotated as **part of a type** or **an interface**:

  ```ts
  interface Screech {
    (): string;
  }
  ```

- An instance of said interface would then be a function thar returns a string:

  ```ts
  declare const scream: Screech;
  const noise = scream(); // 'noise' is inferred as String type
  ```

  > Note: The `declare` keyword here, which I rarely see, is actually used to
  > tell TypeScript that the variable has been created elsewhere. "Elsewhere" here meaning in a
  > different script/file.

- A callable annotation can specify any kind of arguments as well. Optional/Rest arguments can be used without issue here:

  ```ts
  interface LotsOfArguments {
    (foo: string, bar:? number, ...others: boolean[]): number;
  }
  ```

- Not only one callable annotation is supported in an interface, several can actually be specified in the context of function overloading:

  ```ts
  interface Overloaded {
    (foo: string): string;
    (foo: number): number;
  }
  ```

- TypeScript also allows for a simpler arrow type annotation. A function that takes an argument and returns someting can be written as:

  ```ts
  const fun: (foo: number) => string = foo => foo.toString();
  ```

  > We're actually **defining** and **using** the said function in the example above. In the end, the `fun` `const` will have the `foo.toString()` value. Just to clear things up.

- There is a special type of type annotation alled **Newable**, defined by the use of the keyword `new`:

  ```ts
  interface StringGiver {
    new (): string;
  }

  declare const Foo: StringGiver;
  const bar = new Foo(); // Auto inferred as a string type
  ```
