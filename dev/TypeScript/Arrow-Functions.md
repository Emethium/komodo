# Arrow Functions

- Motivations:

  - You don't need to keep writing `function`
  - It lexically captures the meaning of `this`
  - It lexically captures the meaning of arguments

- Reference:

  ```ts
  class Person {
    constructor(public age: number) {}
    growOld = () => {
      this.age++;
    };
  }
  var person = new Person(1);
  setTimeout(person.growOld, 1000);

  setTimeout(function() {
    console.log(person.age);
  }, 2000); // 2
  ```

- You only really need to use it if you are going to give the function to someone else to call.
- If you want `this` to be the calling context, you should probably **do not** use arrow functions.

  - Possible conflicts with libraries that use `this` to pass the object that it is currently iterating over (jquery, underscore, mocha, etc)
  - In this case, if you want to access the library's `this` and the surrounding context, you should wrap the context in a temp variable like:

  ```ts
  let _self = this;
  thing.each(function() {
    console.log(_self); // the scoped value
    console.log(this); // the library passed value
  });
  ```

---

## Arrow functions and inheritance

- Arrow functions can work as classes' properties: (this looks so weird and functional IMO)

```ts
class Adder {
  constructor(public a: number) {}
  add = (b: number): number => {
    return this.a + b;
  };
}
```

- And it works perfectly fine with inheritance:

```ts
class Child extends Adder {
  callAdd(b: number) {
    return this.add(b);
  }
}

const child = new Child(123);
console.log(child.callAdd(123)); // 246
```

- The catch is that it **does not work** with the `super` keyword.
  - So if you try to override a function in a child class, and since properties go on `this`, such functions wouldn't be able to participate in a `super` call.
  - One way to get around is by creating a copy of the method before overriding de child:
  ```ts
  class ExtendedAdder extends Adder {
    // Create a copy of parent before creating our own
    private superAdd = this.add;
    // Now create our override
    add = (b: number): number => {
      return this.superAdd(b);
    };
  }
  ```

---

## Quick object return

- Sometimes you need a function thast just returns a object literal. However, something like the below is parsed **as a block** containing a **JavaScript** label:
  ```ts
  // WRONG WAY TO DO IT
  var foo = () => {
    bar: 123;
  };
  ```
  - And gives you a kind **unused label** TypeScript compilation error :expressionless:
- Strangely, the solution seems to be wrapping the resulting object with `()`:
  ```ts
  // Now it works :smiley:
  var foo = () => ({
    bar: 123
  });
  ```
