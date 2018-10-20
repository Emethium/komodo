# Counter

- Create CSS-maintained variables whose values are incremented by rules defined by CSS:

```html
<ul>
  <li>List item</li>
  <li>List item</li>
  <li>
    List item
    <ul>
      <li>List item</li>
      <li>List item</li>
      <li>List item</li>
    </ul>
  </li>
</ul>
```

```css
ul {
  counter-reset: counter;
}
li::before {
  counter-increment: counter;
  content: counters(counter, '.') ' ';
}
```

- Explanation:
    - The HTML file is rather simple and does not really needs an explanation. Just a unordered list with a sublist.
    - The catch here is that we are going to make numbers appear in each list/sublist element **as they were ordered**.
    - `counter-reset` is used to create or reset a counter, starting with the value 0 as default.
        - The property value is the name of the counter.
    - The `::before` selector inserts content in some element (in our case, the `<li>` tag) **before the element is rendered**.
    - `counter-increment` is used to increase or decrease a defined counter's value
        - Is normally used alongside the `counter-reset` property
        - We could actually decrease it's value if we used `counter-increment: counter - 1`
    - We are going to add generated content to our view by using the `content` property
        - Used alongside with the `::before` and `::after` pseudo-elements
    - `counters(name, string, style)` displays the counter value. The second argument is a string that will be renderer after the counter number.
        - Can also be referred calling `counter(name, string, style)`
        - You do not need to pass all three arguments to the function, only the counter's name is mandatory
        - The `' '` is just used to give a space to the new inserted content