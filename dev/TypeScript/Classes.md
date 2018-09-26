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

##
