# lib.d.ts

- There is a very special file that ships with every TypeScript installation. Yes, the oblivious and not-in-the-title **lib.d.ts**.
- It contains several ambient declarations for common JavaScript constructs present in it's runtime and the infamous DOM.
- So, if we write something like this:
  ```ts
  let foo = 123;
  let bar = foo.toString();
  ```
  - It only **type checks** perfectly **bacause** the `toString` is **defined** in `lib.d.ts`
