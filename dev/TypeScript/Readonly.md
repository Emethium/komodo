# Readonly

- TypeScript's type system allows you to mark individual properties as `readonly`.
- I think that we do not need to state what this does :expressionless:
- It actually allows us to work in a funtional way, since we wouldn't be able to mutate properties.

```ts
function foo(config: { readonly bar: number; readonly bas: number }) {
  // ..
}

let config = { bar: 123, bas: 123 };
foo(config);
// You can be sure that `config` isn't changed
```

- We can also declare `readonly` properties on **Interfaces, Types and Classes** as well.
