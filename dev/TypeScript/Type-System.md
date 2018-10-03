# Type System

- Types are annotated using `:TypeAnnotation` syntax:
  ```ts
  var num: number = 123;
  function identity(num: number): number {
    return num;
  }
  ```
- With the above example we can see how to annotate **variables**, **function parameters** and **function return values**.

---

## Primitive Types

- That would be `string`, `number` and `boolean` as represented below:

  ```ts
  var num: number;
  var str: string;
  var bool: boolean;

  num = 123;
  num = 123.456;
  num = '123'; // Error

  str = '123';
  str = 123; // Error

  bool = true;
  bool = false;
  bool = 'false'; // Error
  ```

---

## Arrays

- You basically have to add an `[]` to any valid annotation to declare an Array (as in `:boolean[]`):

  ```ts
  var boolArray: boolean[];

  boolArray = [true, false];
  console.log(boolArray[0]); // true
  console.log(boolArray.length); // 2
  boolArray[1] = true;
  boolArray = [false, false];

  boolArray[0] = 'false'; // Error!
  boolArray = 'false'; // Error!
  boolArray = [true, 'false']; // Error!
  ```

---

## Interfaces

- It's the core way to compose **multiple type annotations** into a **single one**:

  ```ts
  interface Name {
    first: string;
    second: string;
  }

  var name: Name;
  name = {
    first: 'John',
    second: 'Doe'
  };

  name = {
    // Error : `second` is missing
    first: 'John'
  };
  name = {
    // Error : `second` is the wrong type
    first: 'John',
    second: 1337
  };
  ```

- As we can see, the interface `Name` enforces type checking on individual members, showing the power of the Interface type.

---

## Inline Type Annotation

- Instead of creating a new `interface`, we can annotate anything inline by using the structure `variableName: { /* Structure*/}`. Rewritting the previous example, we would get:

  ```ts
  var name: {
    first: string;
    second: string;
  };
  name = {
    first: 'John',
    second: 'Doe'
  };

  name = {
    // Error : `second` is missing
    first: 'John'
  };
  name = {
    // Error : `second` is the wrong type
    first: 'John',
    second: 1337
  };
  ```

- So, inline types are a great way for quickly providing a one off type annotation for something.
- It saves you the hassle of coming up with a interface or bad type name.
- Buuuut, if you find yourself **reusing the same inline type annotation** over and over again, it's a better idea to **refactor it in a new interface** :wink:

---

## Special Types

### `any`

- `any` is compatible with **any and all types** in the TypeScript type system.
- Which mean that **anything can assigned to it** and **it can be assigned to anything**:

  ```ts
  var power: any;

  // Takes any and all types
  power = '123';
  power = 123;

  // Is compatible with all types
  var num: number;
  power = num;
  num = power;
  ```

- Remeber that it's up to you to ensure the type safety when using the `any` type. As you are telling the compiler to **not do any meaningful static analysis**.

### `null` and `undefined`

- Both of them are actually treated as something of type `any`.
- So these literals can be assigned to any other type:

  ```ts
  var num: number;
  var str: string;

  // These literals can be assigned to anything
  num = null;
  str = undefined;
  ```

- But of course, the two of them have completely different meanings:
  - `undefined` means a **variable has been declared** but has **not yet been assigned a value**
  - `null` is an assignment of the **representation of no value**

### `:void`

- Used to signify that the function does not have a return type:
  ```ts
  function log(message): void {
    console.log(message);
  }
  ```

---

## Generics

- Many algorithms and data structures actually do not depend on the actual type of the object.
- Yet, you still want to enforce a constraint between various variables.
- A simple example is a function that takes a list of something and returns a reversed list of the items:

  ```ts
  function reverse<T>(items: T[]): T[] {
    var toreturn = [];
    for (let i = items.length - 1; i >= 0; i--) {
      toreturn.push(items[i]);
    }
    return toreturn;
  }

  var sample = [1, 2, 3];
  var reversed = reverse(sample); // The `reversed` variable is inferred as being the number[] type here
  console.log(reversed); // 3,2,1

  // Safety!
  reversed[0] = '1'; // Error! We have type safety!
  reversed = ['1', '2']; // Error! We have type safety!

  reversed[0] = 1; // Okay
  reversed = [1, 2]; // Okay
  ```

- The **constraint** here is between **what is passed** to the function and **what is returned by** the function.
- I think it's fairly obvious here, but the Generics here (a.k.a `<T>`) are saying that the `reverse` function:
  - Can take a array of any type
  - Returns an array of type `T`, the same type it takes

---

## Union

- Sometimes you may want to allow a property **to be one of multiple types**.
- We can make use of the union type (denoted by the pipe `|`) to replicate this behaviour:

  ```ts
  function formatCommandline(command: string[] | string) {
    var line = '';
    if (typeof command === 'string') {
      line = command.trim();
    } else {
      line = command.join(' ').trim();
    }

    // Do stuff with line: string
  }
  ```

---

## Intersection

- The `extend` keyword is a fairly known pattern to create a new object that features the characteristics of other objects.
- An Intersection Type in TypeScript allows us to use this pattern in a safe way:

  ```ts
  function extend<T, U>(first: T, second: U): T & U {
    let result = <T & U>{};
    for (let id in first) {
      result[id] = first[id];
    }
    for (let id in second) {
      if (!result.hasOwnProperty(id)) {
        result[id] = second[id];
      }
    }
    return result;
  }

  var x = extend({ a: 'hello' }, { b: 42 });

  // x now has both `a` and `b`
  var a = x.a;
  var b = x.b;
  ```

---

## Tuple

- JavaScript doesn't have tuple support.
- People generally make use of arrays as a tuple, which is exactly what TypeScript supports by anotating arrays with: `:[type1, type2]`:

  ```ts
  var nameNumber: [string, number];

  // Okay
  nameNumber = ['Jenny', 8675309];

  // Error!
  nameNumber = ['Jenny', '867-5309'];
  ```

---

## Alias

- TypeScript provides us a convenient way for providing names for type annotations that you would like to use in several different places.
- The aliases are created by using `type typeName = validTypeAnnotation`:

  ```ts
  type StrOrNum = string | number;

  // Usage: just like any other notation
  var sample: StrOrNum;
  sample = 123;
  sample = '123';

  // Just checking
  sample = true; // Error!
  ```

- Unlike an `interface`, we can give a type alias to literally any type annotation:
  ```ts
  type Text = string | { text: string };
  type Coordinates = [number, number];
  type Callback = (data: string) => void;
  ```
