# Literals

- Literals are **exact values** that are really JavaScript primitives.

## String Literals

```ts
let foo: 'Hello';
```

- Here we hava created a variable called `foo` that will only allow the literal value `'Hello'` to be assigned. So, this actually happens:

  ```ts
  let foo: 'Hello';
  foo = 'Bar'; // Error: "Bar" is not assignable to type "Hello"
  ```

- They can be used in a type union to create abstractions:

  ```ts
  type CardinalDirection = 'North' | 'East' | 'South' | 'West';

  function move(distance: number, direction: CardinalDirection) {
    // ...
  }

  move(1, 'North'); // Okay
  move(1, 'Nurth'); // Error!
  ```

  > Seems useful.

---

## Other literal types

- We can make such abstractions with `boolean` and `number` types:
  ```ts
  type OneToFive = 1 | 2 | 3 | 4 | 5;
  type Bools = true | false;
  ```
