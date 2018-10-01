# For...of

- The `for...of` of TypeScript (and ES6) is used to iterate over elements of an array, as can be seen on:
  ```ts
  const array = [3, 5, 7];
  for(let item of array) {
    console.log(item);  // 3, 5, 7
  }
  ```

- One common **mistake** seems to misunderstand the mentioned construction with `for...in`, but they are not equivalent.
  - `for...in` actually **iterates over the array's keys**, not the array's objects. So the adapted version of the code above would produce a different output:
  ```ts
  const array = [3, 5, 7];
  for(let item of array) {
    console.log(item);  // 0, 1, 2
  }
  ```