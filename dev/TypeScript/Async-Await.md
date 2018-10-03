# Async Await

- As an experiment, let's try to tell the JavaScript runtime to **pause** the code execution on the use of the `async` keyword, return once and only if a promise is succeded.
- It's **not actual code** gentleman, just the idea:
  ```ts
  async function foo() {
    try {
      var val = await getMeAPromise();
      console.log(val);
    } catch (err) {
      console.log('Error: ', err.message);
    }
  }
  ```
- So, two things to note:
  - If the promise has been fullfilled, then `await` will return the value
  - If not, an error will be thrown synchronouly
- This structure magically makes asynchronous programming as easy as synchronous programming.
- So, three things are needed for this concept:
  - The ability to **pause function execution**
  - The ability to put a value inside the function
  - The ability to throw and exception inside the function

---

## TypeScript implementation

```ts
function delay(milliseconds: number, count: number): Promise<number> {
  return new Promise<number>(resolve => {
    setTimeout(() => {
      resolve(count);
    }, milliseconds);
  });
}

// async function always returns a Promise
async function dramaticWelcome(): Promise<void> {
  console.log('Hello');

  for (let i = 0; i < 5; i++) {
    // await is converting Promise<number> into number
    const count: number = await delay(500, i);
    console.log(count);
  }

  console.log('World!');
}

dramaticWelcome();
```
