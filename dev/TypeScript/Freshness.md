# Freshness (a.k.a _strict object literal checking_)

- It's a concept provided to us by TypeScript to make object literals type checking easier.
- Consider the following piece of code:

  ```ts
  function logName(something: { name: string }) {
    console.log(something.name);
  }

  var person = { name: 'matt', job: 'being awesome' };
  var animal = { name: 'cow', diet: 'vegan, but has milk of own species' };
  var random = { note: `I don't have a name property` };

  logName(person); // okay
  logName(animal); // okay
  logName(random); // Error: property `name` is missing
  ```

- Strangely it passes the notion that something accepts more data than it actually does:

  ```ts
  function logName(something: { name: string }) {
    console.log(something.name);
  }

  logName({ name: 'matt' }); // okay
  logName({ name: 'matt', job: 'being awesome' }); // Error: object literals must only specify known properties. `job` is excessive here.
  ```

  > That does only ever happen when we are dealing with object literals.
