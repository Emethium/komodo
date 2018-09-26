# References

- All Objects in JavaScript are references, which means:

---

### Mutations can occur across references

```ts
var person = {};
var guy = person; // guy is referencing the same object as person

person.name = 'John Doe';
console.log(guy.name); // 'John Doe' will be printed out, since it's the same reference
```

### Object equality work for references

```ts
var person = {};
var guy = person; // guy is referencing the same object as person
var other_guy = {}; // other_guy here is a new object with a different reference

console.log(person === guy); // true, since it's the same reference
console.log(person === other_guy); // false, since they have not the same reference
```
