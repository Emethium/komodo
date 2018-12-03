# Functional Programming in JavaScript

## Pure functions

- What defines a **pure function**?

  - It always returns the same result if given the same arguments (also called _deterministic_)
  - It does not cause any observable side effects

- **It always returns the same result if given the same arguments**

  - Imagine we want to implement a function that calculates the area of a circle:

  ```js
  const PI = 3.14;

  function calculateArea(radius) {
    return radius * radius * PI;
  }

  calculateArea(10); // returns 314.0
  ```

  - But this is **not a pure function**. And why is that?

    - Since it **used a global object** that was **not passed as a parameter** to the function, it **cannot be called pure**.
    - So if we change the global `PI` value to `42`, for example, that would result in `4200`. We would have got a different result with the same parameters! (`radius` = 10)

  - But we can easily fix that:

  ```js
  const PI = 3.14;

  function calculateArea(radius, pi) {
    return radius * radius * pi;
  }

  calculateArea(10, PI); // returns 314.0
  ```

  - Since we always pass the `PI` value as a parameters, all the parameters are feed to the function without external object interference. **Now we can say we have a pure function**.

- **Reading files**

  - If our function reads external files, it cannot be a pure function **as the file's contents can change**.

- **Random number generation**

  - Any function that **relies** on random number generation cannot be pure.

- **It does not cause any observable side effects**

  - Examples of "Observable side effects" include: modifying a global object or a parameter passed by reference.
  - If we implement a function to recieve an integer value and return the value increased by 1:

  ```js
  let counter = 1;

  function increaseCounter(value) {
    counter = value + 1;
  }

  increaseCounter(counter);
  console.log(counter); // 2
  ```

  - The issue here is that our impure function recieves the value but re-assigns the outerly scoped `counter` with it's value increased by one. In other words, we modified a global object so our function **cannot be called pure**.
  - Transforming our function into a pure one is a very simple task, tho:

  ```js
  let counter = 1;

  function increaseCounter(value) {
    return value + 1;
  }

  increaseCounter(counter); // 2
  console.log(counter); // 1
  ```

  - Now our **function is pure**. We do not change the global scoped variable anymore, just returning the increment of it's value.

- **Pure functions benefits**
  - Functions are isolated and are unable to impact in other parts of our system
  - Given the same parameters, pure functions always return the same value
  - We don't need to think of situations when the same parameters have different results **as they will never happen**
  - Easier to test code

## Immutability

- We refer here to our inability to change an object after it's created. **Instead, we create a new object with a new value**.
- The following `for` loop has some mutable variables:

```js
let values = [1, 2, 3, 4, 5];
let sumOfValues = 0;

for (int i = 0; i < values.length; i++) {
  sumOfValues += value[i];
}

console.log(sumOfValues); // 15
```

- In each `for` iteration we are changing the `i` and `sumOfValues` states. And how we deal with immutability in a iteration? **Recursion!**

```js
let list = [1, 2, 3, 4, 5];
let accumulator = 0;

function sum(list, acc) {
  if (list.length == = 0) {
    return acc;
  } else {
    return sum(list.slice(1), acc + list[0]);
  }
}

sum(list, accumulator); // 15
console.log(list);  // [1, 2, 3, 4, 5]
console.log(accumulator); // 0
```

- Fun, isn't it? Here we **never reassigned any of the former variables** but obtained the final answer **by manipulating values in memory inside our recursive function**! The global variables values stayed as they were.

## Referential transparency

- Consider the following `square` function:

```js
function square(n) {
  return n * n;
}
```

- It's a **pure function** that will always return the same output, given the same input. Passing `2` as a parameter will always return `4`, as we could replace `square(2)` with `4`. Our function is **referentially transparent**.

- **pure functions + immutable data = referential transparency**

## Functions as first-class entities

- The concept of functions as first-class entities is that **functions are also treated as values and used as data**

- Functions as first-class entities can:

  - Refer to it from constants and variables
  - Pass it as parameters to other functions
  - Return it as result from other functions

- We should **treat functions as values** and **pass functions like data**.

- Imagine we have a function that sums two values and then doubles it, and another that subtracts those same values and returns the double:

```js
function doubleSum(a, b) {
  return (a + b) * 2;
}

function doubleSub(a, b) {
  return (a - b) * 2;
}
```

- Both functions follow a similar logic, being the only difference the operators used. If we treat **functions as values** and **pass along as arguments**, we can **build a function** that receives the operator function and use it inside itself:

```js
function sum(a, b) {
  return a + b;
}

function sub(a, b) {
  return a - b;
}

function doubleOperator(f, a, b) {
  return f(a, b) * 2;
}

doubleOperator(sum, 3, 1); // 8
doubleOperator(sub, 3, 1); // 4
```

- It can be a little confusing at first, but it's really simple. We're using **a third function as a function-builder** to apply the common pattern between our former two functions (the `* 2` operation) by passing along the `sum` or `sub` functions.

- Remember that the objective here was to **treat functions as values** and **pass them along as arguments**!

## Higher-order functions

- When we are talking about such functions we refer to a function that either:

  - Takes one or more functions as arguments
  - Returns a function as a result

- As a matter of fact we just did one of the kind! THe `doubleOperator` function is a higher-order one because it takes one function as an argument an uses it to produce an output.

- We will cover now the famous `filter` and `map` as examples. Let's take a look.

- **Filter**

  - Given a collection, we want to filter it by an attribute. The filter function expects a `true` or `false` value do determine if the element **should or not** be included in the result collection.
  - In other words, if the callback expression is `true`, the `filter` function will include the element on the collection. Otherwise, it will not.
  - A declarative JavaScript example would be:

  ```js
  let numbers = [10, 9, 8, 7, 6, 5, 1, 3, 0];

  function smaller(number) {
    return number < this;
  }

  function filterArray(x, list) {
    return list.filter(smaller, x);
  }

  filterArray(3, numbers); // [1, 0]
  ```

  - Some explanation is needed to clarify things. `this` will be the second parameter in the `filter` function, being the `x` in our `.filter` call.

- **Map**

  - The `map` method transforms a collection by applying a function to all of its elements and building a new collection from the returned values.

  ```js
  let values = [1, 2, 3, -4, 5];

  function updateListByMap(values) {
    return values.map(Math.abs);
  }

  updateListByMap(values); // [1, 2, 3, 4, 5];
  ```
