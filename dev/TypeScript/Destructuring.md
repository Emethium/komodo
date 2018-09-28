# Destructuring

- **Destructuring** (which may be parsed as "break up the structure") may refer to:
  - Object Destructuring
  - Array Destructuring
- You may see this process as the **inverse of structuring**, the latter being the example below:
  ```ts
  var foo = {
    bar: {
      bas: 123
    }
  };
  ```

---

## Object Destructuring

- If we think about it, **object structuring** in JavaScript/TypesScript would be the "process of structuring an object based on attributes", am I right?
- So, if we think the opposite way, **object destructuring** wouldn't really be "the dismantle of an object" but **"the process of structuring attributes based on an object"**
- Which can be fairly understood by the code below:

  ```ts
  var rect = { x: 0, y: 10, width: 15, height: 20 };

  // Destructuring assignment
  var { x, y, width, height } = rect;
  console.log(x, y, width, height); // 0,10,15,20

  rect.x = 10;
  ({ x, y, width, height } = rect); // assign to existing variables using outer parentheses
  console.log(x, y, width, height); // 10,10,15,20
  ```

- As you can see, it allows us to do in a **single line** what we would have done in **four lines**.
- We can also extract a variable into **a new variable name** using the same method:

  ```ts
  // structure
  const obj = { 'some property': 'some value' };

  // destructure
  // we're setting the 'some property' value of 'obj' to a const variable named 'someProperty'
  const { 'some property': someProperty } = obj;
  console.log(someProperty === 'some value'); // true
  ```

- When we're dealing with **Rest Parameters**, we can get any number of the object's parameters and extract of the remaining elements, such as:
  ```ts
  var { w, x, ...remaining } = { w: 1, x: 2, y: 3, z: 4 };
  console.log(w, x, remaining); // 1, 2, {y:3,z:4}
  ```
  - We can use this strategy to ignore object properties in a case of need:
    ```ts
    // Example function
    function goto(point2D: { x: number; y: number }) {
      // Imagine some code that might break
      // if you pass in an object
      // with more items than desired
    }
    // Some point you get from somewhere
    const point3D = { x: 1, y: 2, z: 3 };
    // So here we are creating a point2D const with the 'x' and 'y' properties
    // of the point3D object. We're just excluding the 'z' member
    const { z, ...point2D } = point3D;
    goto(point2D);
    ```

---

## Array Destructuring

### Array Destructuring with Rest

```ts
// That's really straightforward, based on what we already discussed
var [x, y, ...remaining] = [1, 2, 3, 4];
console.log(x, y, remaining); // 1, 2, [3,4]
```

### Array Destructuring with ignores

- You can ignore elements by leaving and empty space between commas (`, ,`), just like:

```ts
var [x, , ...remaining] = [1, 2, 3, 4];
console.log(x, remaining); // 1, [3,4]
```
