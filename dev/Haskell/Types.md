# Types

## `Int`

- Stands for integer.
- Used for whole numbers, meaning that it applies do `10`, but naturally won't be the applied type for `10.1`
- It is bounded, meaning it has a minimum and maximum value to be defined by the `Bounded` class
    - **Bounded classes** are used to name the upper and the lower limits of a type
    - In our dear `Int` case, we can use:
        - `Int8` do declare 8-bit Integers
        - `Int16` do declare 16-bit Integers
        - `Int32` do declare 32-bit Integers
        - `Int64` do declare 64-bit Integers

## `Integer`

- It looks funny, bit it also stands for a integer :wink:
- The difference here is that `Integer` **is not bounded**, so it can be used to represent any range of numbers, even reeeeeeealy big ones:
    ```haskell
    factorial :: Integer -> Integer  
    factorial n = product [1..n] 

    ghci> factorial 50
    30414093201713378043612608166064768844377641568960512000000000000
    ```

## `Float`

- Easy enough, a floating point with single precision:
  ```haskell
  circumference :: Float -> Float  
  circumference r = 2 * pi * r

  ghci> circumference 4.0  
  25.132742  
  ```

## `Double`

- Ehr, a floating point with double precision:
  ```haskell
  circumference' 4.0  
  25.132741228718345
  ```

> Upon wirting this, I didn't know the definition difference between **single** and **double** precision when dealing with floating point numbers. I found out that it's a contextual misnomer, meaning that the **double precision number takes twice as many bits** than it's single point counterpart, **not really two times the number as the name would imply.**


## `Bool`

- Boolean type. Can have only one of two values: `True` and `False`


## `Char`

- Represent a character
- Denoted by single quotes (aka `''`)
- A list of characters is a `String` (which is something called **Type Synonym** for a `[Char]`)

> Haskell provides a way to define *type synonyms* for convenience sake. They do not define new types, but simply give new names for existing ones, as: `String` for `[Char]`, `Person` for `(Name, Address)`

## Tuples

- Tuples are also types, but they are dependent on their length and the types of their components.
- Meaning, theoretically, there are an infinite number of tuples.
- Tuples are written bu the use of parenthesis with any elements inside: `(Integer, String)`
- The **empty tuple** `()` is also a type which can have a single (and empty) value;

## Type variables

- Let's check the type definition of the `head` function:
  ```haskell
  ghci> head
  head :: [a] -> a
  ```
- What is this `a`? Is it a type?
  - Not really. Since it's not written in capital case, it can't exactly be a type.
  - It's actually a **type variable** than can be of **any type**
  - This is much like generics in other languages, only in Haskell it's much more powerful because it allows us to easily write very general functions
  - So, the type definition of `head` states that it takes  **a list of any type** and returns one element of that list.