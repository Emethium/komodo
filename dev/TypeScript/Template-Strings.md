# Template Strings

- They are string represented by backticks (aka -> `) instead of single or double quotes.
- Commonly used for the purpose of:
  - String Interpolation
  - Multiline Strong
  - Tagged Templates

---

## String Interpolation

- Let's say you want to generate a string out of some static strings and variables, which is really common.
- On a first try, you would propably think of something like this:
  ```ts
  const lyrics = `Never gonna give you up`;
  let html = `<div>` + lyrics + `</div>`;
  ```
- But properly using template strings, you can just do:
  ```ts
  const lyrics = `Never gonna give you up`;
  let html = `<div>${lyrics}</div>`;
  ```
  - It's important do note that anything inside the interpolation `${}` is **treated like a JavaScript expression** and **evaluated**. Meaning that **math** also works:
    ```ts
    console.log(`1 and 1 make ${1 + 1}`); // '1 and 1 make 2'
    ```

---

## Multiline Strings

- In case you needed to put a **newline** in JavaScript, you would have probably needed to use a **literal newline** to escape a string using the escape character `\` folowed by the newline `\n`:
  ```ts
  var lyrics =
    'Never gonna give you up \
  \nNever gonna let you down';
  ```
- But in TypeScript you can simply:
  ```ts
  var lyrics = `Never gonna give you up
  Never gonna let you down`;
  ```

---

## Tagged Templates

- It's possible to place a function (called `tag`) before the template string in order to pre process the template literals and placeholder expressions. Example:

  ```ts
  var say = 'a bird in hand > two in the bush';
  var html = htmlEscape`<div> I would just like to say : ${say}</div>`;

  // a sample tag function
  function htmlEscape(literals: TemplateStringsArray, ...placeholders: string[]) {
    let result = '';

    // interleave the literals with the placeholders
    for (let i = 0; i < placeholders.length; i++) {
      result += literals[i];
      result += placeholders[i]
        .replace(/&/g, '&amp;')
        .replace(/"/g, '&quot;')
        .replace(/'/g, '&#39;')
        .replace(/</g, '&lt;')
        .replace(/>/g, '&gt;');
    }

    // add the last literal
    result += literals[literals.length - 1];
    return result;
  }
  ```

- Things to note:
  - All the **static literals** are passed in as an array for the **first argument**
  - All the values of the placeholders are passed in as the remaining arguments

> Placeholder can actually be any kind of `[]`, but they will be type checked by TypeScript.
> So, if you expect do deal with a `string` or a `number` you should annotate something like:
> `...placeholders:(string | number)[]`
