# JSON

## Parsing `JSON`
- The `parse` method takes only two arguments: **a string representing a `JSON` value** and **an optional `reviver` function**
- Normally, we would use just the first argument to parse the value, which works just fine:
```js
const json = '{'key': 'value'}';
const value = JSON.parse(json);
```
- But what about the `reviver` argument?
  - By definition, `reviver` is a function to be passed to every key in the JSON object, transforming the object by replacing every value with a different one.
  - The funny thing is that the function will be applied to every key in the JSON object, no matter how deep the value is. This allows the same `reviver` function to run in different JSON files altogether.
