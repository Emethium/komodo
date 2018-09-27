# Rest Parameters

- Rest parameters are treated as a boundless number of optional parameters.
- You can use as many as you want, or pass none.
- The compiler will build an array of the arguments passed in with the **name given after the elipsis** (...)
- Reference:

  ```ts
  function iTakeItAll(first, second, ...allOthers) {
    console.log(allOthers);
  }

  iTakeItAll('foo', 'bar'); // [], as 'allOthers' is set after the third argument
  iTakeItAll('foo', 'bar', 'bas', 'qux'); // ['bas','qux']
  ```
