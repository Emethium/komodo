# Classes

## General example

```ts
class Point {
  x: number;
  y: number;
  constructor(x: number, y: number) {
    this.x = x;
    this.y = y;
  }
  add(point: Point) {
    return new Point(this.x + point.x, this.y + point.y);
  }
}

var p1 = new Point(0, 10);
var p2 = new Point(10, 20);
var p3 = p1.add(p2); // {x:10,y:30}
```

---

## Inheritance

- Classes in TypeScript, as in many other languages, support inheritance using the `extends` keyword.
- The bahaviour is the same as you might expect, nothing more.

---

## Statics

- **Static** properties in classes are shared among all instances of that class.
- In other words:

```ts
class Something {
  static instances = 0;
  constructor() {
    Something.instances++;
  }
}

var s1 = new Something();
var s2 = new Something();
console.log(Something.instances); // 2
```

- The same behaviour can be obtained with functions, using `static functions`.

---

## Access Modifiers

- TypeScript supports the following access modifiers:
  - `public`
  - `private`
  - `protected`
- If a access modifier is not set, a `public` one will be implicitally set.
- In the compiled JS, access modifiers pose no significance, but will give compile errors when used incorrecly :grimacing:
- The class accessibility reference is shown below:

| Accessible on   | `public` | `protected` | `private` |
| --------------- | -------- | ----------- | --------- |
| class           | yes      | yes         | yes       |
| class children  | yes      | yes         | no        |
| class instances | yes      | no          | no        |

---

## Abstract

- Abstract classes or members works as access modifiers, but within a different context.
- The `abstract` modifier implies that a dafined class or member cannot be directly invoked or instantiated.
  - Abstract **classes** cannot be directly instantiated, so you must make use of a child class that inherits the former in order to use it.
  - Abstract **members** cannot be directly invoked, so a child class must provide the method functionality. 

---

## Constructor

- Completely optional, you don't need to specify one for a class. Therefore, the following is perfctly valid: :smirk: 
  ```ts
  class Thing {}
  let thing = new Thing();
  ```
- Initialing member classes in constructors (with the specific access modifiers) can be simplified. So the following code:
  ```ts
  class Thing {
    x: number;
    constructor(x: number) {
      this.x = x;
    }
  }
  ```
  - Can be rewritten as:
  ```ts
  class Thing {
    constructor(public x:number) {
    }
  }
  ```
  - I personally have some issues regarding legibility of the second option, but that's up to you.

---

## Property initializer
- Class members can actually be initialized outside the constructor, so the following would be valid:
  ```ts
  class Thing {
    stuff = [];  // Here you go
    add(x) {
      this.stuff.push(x);
    }
  }
  ```