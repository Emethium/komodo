# Enums

- An `enum` is a way to organize a collection of values:

  ```ts
  enum Pokemon {
    Bulbasaur,
    Squirtle,
    Charmander,
    Pikachu
  }

  let pkmn = Pokemon.Bulbasaur;
  pkmn = 'not a pokémon'; // Error : string is not assignable to type `Pokemon`
  ```

---

## Number Enums and Numbers

- TypeScript enums are number-based, which means that numbers can be assigned to an instance of the enum.
- Also means that anything is compatible with `number`:

  ```ts
  enum Color {
    Red,
    Blue,
    Yellow
  }

  let col = Color.Red;
  col = 0; // The same as Color.Red
  ```

---

## Number Enums and Strings

- I was going to write some explanation here, but I think the piece of code below is **self-explanatory**:
  ```ts
  console.log(Color[0]); // "Red"
  console.log(Color['Red']); // 0
  console.log(Color[Color.Red]); // "Red"
  ```
  :grin:

---

## Changing the number associated with a Number Enum

- By default, as we already realized by this point, the enum's number values start as `0` and have a increased value of `1` on each new element.
- As have we already stated:
  ```ts
  enum Pokemon {
    Bulbasaur, // 0
    Squirtle, // 1
    Charmander, // 2
    Pikachu // 3
  }
  ```
- Those values can be changed by specifically setting them inside the `Enum`. The following elements will have the `1` value increment, as we have seen before:
  ```ts
  enum Pokemon {
    Bulbasaur = 3, // 3
    Squirtle, // 4
    Charmander, // 5
    Pikachu //6
  }
  ```

---

## String Enums

- We've mainly discussed about `Enum` members associated with numerical values, but they can have `string` values associated as well:
  ```ts
  export enum EvidenceTypeEnum {
    UNKNOWN = '',
    PASSPORT_VISA = 'passport_visa',
    PASSPORT = 'passport',
    SIGHTED_STUDENT_CARD = 'sighted_tertiary_edu_id',
    SIGHTED_KEYPASS_CARD = 'sighted_keypass_card',
    SIGHTED_PROOF_OF_AGE_CARD = 'sighted_proof_of_age_card'
  }
  ```
- Of course, there is no auto-increment in member's values when we're dealing with them as strings. Wouldn't make much sense, would it?
- The main use would be in string comparations:
  ```ts
  const value = someString as EvidenceTypeEnum;
  if (value === EvidenceTypeEnum.PASSPORT) {
    console.log('You provided a passport');
    console.log('value'); //  'passport'
  }
  ```

---

## Const Enums

- I found this as pretty funny, to tell you the truth.
- If you have a enum like:

  ```ts
  enum Tristate {
    False,
    True,
    Unknown
  }

  var lie = Tristate.False;
  ```

- The last line is actually compiled as `var lie = Tristate.False`. **Yes** the compiled JavaScript code is the same as the written TypeScript code. But what does that mean?
- It means the **runtime needs to lookup** `Tristate` and then `Tristate.False`. But we can actually get a **performance boost here** if we take this necessity away from the runtime.
- And how we do that? Marking the `enum` as a `const enum`:

  ```ts
  const enum Tristate {
    False,
    True,
    Unknown
  }

  var lie = Tristate.False;
  ```

- This generates the following JavaScript code: `var lie = 0;`. Which is, of course, more perfomant.

---

## Enum with static functions

- By using the combo: `enum` + `namespace` we can merge static methods inside an enum:

  ```ts
  enum Weekday {
    Monday,
    Tuesday,
    Wednesday,
    Thursday,
    Friday,
    Saturday,
    Sunday
  }
  namespace Weekday {
    export function isBusinessDay(day: Weekday) {
      switch (day) {
        case Weekday.Saturday:
        case Weekday.Sunday:
          return false;
        default:
          return true;
      }
    }
  }

  const mon = Weekday.Monday;
  const sun = Weekday.Sunday;
  console.log(Weekday.isBusinessDay(mon)); // true
  console.log(Weekday.isBusinessDay(sun)); // false
  ```

- That's what I read, but I did not see this as a big deal, since it would also work for any other valid type and object :confused:

---

## Enums are open ended

- As this section's title elucidates, enums can be extended and altered without any problem. Even in multiple files.
- Something like this would generate an enum with **all** members included:

  ```ts
  enum Color {
    Red,
    Green,
    Blue
  }

  enum Color {
    DarkRed,
    DarkGreen,
    DarkBlue
  }
  ```
