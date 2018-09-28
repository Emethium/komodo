# The Spread Operator

- It seems to be best explained by examples, so let's try that.

## Apply

- One use of the spread operator is to **spread array elements into function arguments**.
- So, if we try to think a method of doing what I've stated above, we would probably think of something like this:

  ```ts
  function foo(x, y, z) {}

  const stuff = [0, 1, 2];
  foo.apply(null, stuff);
  ```

- But we can actually do something like this with the spread operator, with the same effect:

  ```ts
  function foo(x, y, z) {}

  const stuff = [0, 1, 2];
  foo(...stuff);
  ```

---

## Destructuring

- We have a proper **file** to talk about this issue, but we can make use of the spread operator to to capture the remaining elements of an array:
  ```ts
  let [x, y, ...remaining] = [1, 2, 3, 4];
  console.log(x, y, remaining); // 1, 2, [3, 4]
  ```

---

## Array Assignment

- Here we can use the spread operator to create expanded versions of arrays. That's really simple, really:
  ```ts
  let list = [1, 2];
  list = [...list, 3, 4];
  console.log(list); // [1, 2, 3, 4]
  ```
- It can also be done in any position, so the following would also be valid:
  ```ts
  var list = [1, 2];
  list = [0, ...list, 3];
  console.log(0, 1, 2, 3); // [0, 1, 2, 3]
  ```

---

## Object Spread

- The same principle we've seen on arrays can actually be used to spread objects into another:
  ```ts
  const some = { x: 1, y: 2 };
  const thing = { ...some, z: 3 }; // You get the idea
  ```
- But the catch here is that the **order really matters**, causing attributes do be overwritten:

  ```ts
  const something = { x: 1, y: 2 };
  // Since we're inserting another 'x' attribute in a later position, the value that was '5'
  // will actually be overwritten by '1' of the 'something' object
  const anotherThing = { x: 5, z: 4, ...something };
  console.log(anotherThing); // {x: 1, y: 2, z: 4}

  // Now it's the opposite. Since we're assigning the value '5' for 'x' AFTER including
  // the 'something' object, the latter attribute 'x' value will be overwritten by '5'
  const yetAnotherThing = { ...something, x: 5, z: 4 };
  console.log(yetAnotherThing); // {x: 5, y: 2, z: 4}
  ```
