# Null and Undefined

- **Null**: When referring to something that **isn't available**.
- **Undefined**: WHen referring to something that **hasn't been initialized**.

---

## Equality

```js
console.log(undefined == undefined); // true, undefined equals undefined
console.log(null == undefined); // true, something not initialized surely isn't avaliable
console.log(0 == undefined); // false, 0 is a number, not undefined
console.log('' == undefined); // false, '' is a string, not undefined
console.log(false == undefined); // false
```

- Checking for `== null` actually checks for both **undefined** or **null**.
