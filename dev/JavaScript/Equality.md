# Equality

---

## General

- JavaScript does **not** try to do **type coercion** when we use **double equality ('==')**.
  - So the following would be true:
  ```ts
  console.log(9 == '9'); // true
  ```
- The **triple equlity ('===')**, on the other hand, **tries** to do **type coercion** on equalities.
  - So the following would be true:
  ```ts
  console.log(9 === 9); // true
  ```
  - And the following wouldn't:
  ```ts
  console.log(9 === '9'); // false =/
  ```
- There are some funny things, tho.
  - If you try to compare "" and "0", since they are different strings, they would naturally return **false** on double equality:
  ```ts
  console.log('' == '0'); // false
  ```
  - But as **0** and **""** both behave as **false** on JS, the following would return **true**:
  ```ts
  console.log(0 == ''); // true
  ```
  - What wouldn't really happen with triple equality, since the types are different:
  ```ts
  console.log(0 === ''); // false
  ```

> Noting that comparations between different data types, such as **string == number** and **string === number** that we've seen above would result in compile errors in TypeScript :relaxed:

> PROTIP: always use **===** and **!==**, except for null checks

---

## Structural

- If we want to compare two objects, we should not use **==** or **===** as they are not sufficient.
  - For instance, you may think they would work, bur the following would return false:
  ```ts
  console.log({ label: 'name' } == { label: 'name' }); // false
  console.log({ label: 'name' } === { label: 'name' }); // false
  ```
- In most cases we will want to compare objects by some specific attribute (and id, for example), but if you really really want to check for the whole object, you'll probably want to use the [deep-equal npm package](https://www.npmjs.com/package/deep-equal).
