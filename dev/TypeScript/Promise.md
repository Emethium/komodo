# Promise

- The main motivation for the use of `Promise` is to bring **synchronous** style error handling to **Async / Callback** style code.

- A promise can be either:

  - `pending`
  - `fulfilled`
  - `rejected`

- The `promise` can be subscribed using `.then` (if resolved) or `.catch` (if rejected):
  ```ts
  const promise = new Promise((resolve, reject) => {
    resolve(123);
  });
  promise.then(res => {
    console.log('I get called:', res === 123); // I get called: true
  });
  promise.catch(err => {
    // This is never called
  });
  ```

---

## Chain-ability of Promises

- You can use `.then` to create a chain of of promises:
  ```ts
  Promise.resolve(123)
    .then(res => {
      console.log(res); // 123
      return 456;
    })
    .then(res => {
      console.log(res); // 456
      return Promise.resolve(123); // Notice that we are returning a Promise
    })
    .then(res => {
      console.log(res); // 123 : Notice that this `then` is called with the resolved value
      return 123;
    });
  ```
- You can aggregate the error handlng into a single `catch`:
  ```ts
  Promise.reject(new Error('something bad happened'))
    .then(res => {
      console.log(res); // not called
      return 456;
    })
    .then(res => {
      console.log(res); // not called
      return 123;
    })
    .then(res => {
      console.log(res); // not called
      return 123;
    })
    .catch(err => {
      console.log(err.message); // something bad happened
    });
  ```
- The `catch` actually **returns a new promise**, creating a new promise chain:
  ```ts
  Promise.reject(new Error('something bad happened'))
    .then(res => {
      console.log(res); // not called
      return 456;
    })
    .catch(err => {
      console.log(err.message); // something bad happened
      return 123;
    })
    .then(res => {
      console.log(res); // 123
    });
  ```
- The `catch` is only called if an error occurs in the preceding chain:
  ```ts
  Promise.resolve(123)
    .then(res => {
      return 456;
    })
    .catch(err => {
      console.log('HERE'); // never called
    });
  ```
