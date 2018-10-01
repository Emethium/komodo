# Iterators

- Iterators are **not** considered a **TypeScript or an ES6 feature**, but a **Behavioral Design Pattern** common for object-oriented programming languages.
- It's normally an object that implements the following interface:
  ```ts
  interface Iterator<T> {
    next(value?: any): IteratorResult<T>;
    return?(value?: any): IteratorResult<T>;
    throw?(e?: any): IteratorResult<T>;
  }
  ```
- We can see that the iterator will be used to retreive values from some kind of collection.
- The iterator result is simply a `value` + `done` pair:
  ```ts
  interface IteratorResult<T> {
    done: boolean;
    value: T;
  }
  ```

---

## Motivation

- Iterator behaviour can commonly be achieved without the implementation of said structure. But there are a couple of reasons why you should actually use it:

  - Interfaces have **zero** impact in the JacaScript runtime
  - Structures can be easly modified because **TypeScript interfaces are open ended**. Which means we can add new members simply by:

  ```ts
  // Lib a.d.ts
  interface Point {
      x: number; y: number;
  }
  declare var myPoint: Point;

  // Lib b.d.ts
  interface Point {
      z: number;
  }

  // Your code
  var myPoint.z; // Allowed!
  ```

  - Offers more code consistency

---

## Iterable protocol

- The ES6 defines the _iterable protocol_, which includes th **[Symbol.iterator]** if the iterable interface is implemented:

  ```ts
  class Frame implements Iterable<Component> {
    constructor(public name: string, public components: Component[]) {}

    [Symbol.iterator]() {
      let pointer = 0;
      let components = this.components;

      return {
        next(): IteratorResult<Component> {
          if (pointer < components.length) {
            return {
              done: false,
              value: components[pointer++]
            };
          } else {
            return {
              done: true,
              value: null
            };
          }
        }
      };
    }
  }

  let frame = new Frame('Door', [
    new Component('top'),
    new Component('bottom'),
    new Component('left'),
    new Component('right')
  ]);
  for (let cmp of frame) {
    console.log(cmp);
  }
  ```

- There are some things to be noted here:
  - **Symbols** are a primitive data type, created by calling the `Symbol` constructor
  - **Symbol.iterator** is a method that returns the default iterator for an object
