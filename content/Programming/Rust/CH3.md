---
id: CH3
aliases:
  - CH3
tags: []
---

# CH3

## Variables and Mutability

By default, vars are immutable, meaning they cannot change.
this ensures safety and concurrency

There is still the optino to make the variable mutable with the `mut` keyword

ex:

```rust
fn main() {
  let mut x = 5; // this can change
  let y = 6; // this cannot change
  println!("{x}") // 5
  x = 7;
  println!("{x}") // 7
  y = 8; // Error
}
```

### Constants

constants are values that are bound to a name and are not allowed to change, but they cannot have `mut` added to make it mutable. The keyword for it is `const`

```rust
const THREE_HOURS_IN_SECONDS: u32 = 60 * 60 * 3;
```

### Shadowing

Shadowing is setting a variable to itself, assuming it was already set before:

```rust
fn main(){
  let x = 5;

  let x = x + 1; // Shadowing

{
    let x = x * 2;
    println!("The value of x in the inner scope is: {x}");
  }
  println!("The value of x is {x}");
}
```

the main differenc between shadowing and `mut` is that a new variable is set, so the type of the variable can be changed as well.

## Data Types

The type of the variable has to be set when it is made, because rust is statically typed

### Scalar Types

Rust has four primary scalars:

1. Integer
2. Floating Point Number
3. Boolean
4. Character

#### Integer Types

An integer is a number without a fractional component

![Rust_IntTypes.png](Rust_IntTypes.png)

Each signe int can store numbers from $-(2^{n-1})$ to $2^{n-1}$ inclusive. $n$ is the number of bits that it uses, so an i16, with 16 bits, stores from $-(2^15)$ to $2^15)$ which is -32,768 to 32,767.

![Rust_IntLit.png](Rust_IntLit.png)

#### Integer Overflow

an int overflow happens when you attempt to set an integer to something larger than is allocated. when debug compiling the program will panic, but when the release build is made, the int will just wrap back down, eg 256 = 0, 257 = 1. this is incorrect behaviour.

#### Floating Point Types

Rust has `f32` and `f64`, the number is the number of bits in the size.

#### The Boolean Type

Just a basic binary `true` and `false`

#### The Character Type

Single alphabetical character. specified with single quotes

### Compound Types

Compound types group multiple values, the two primitive types are:

1. Tuples
2. Arrays

#### Tuple Type

general way of grouping together a number of values with different types into one compound type. they have a fixed length, once declared they cannot grow or shrink in size.

#### Array Type

In an array, all values have the same type, and they also have a fixed length.

arrays are allocated on the stack, arrays are more for whe you know the number of elements will not change.

## Functions

defined using the `fn` keyword, they should be named using snake case, all lowervase and underscores used.

### Parameters

these are passed just like most other languges

### Statements and Expressions

Statements are instructions that perform some action and do not return a value

Expressions evaluate to a resultant value

### Functions with Return Values

the syntax for declaring the type of returned value is `->`. this is placed just after args and before the `{`.

## Comments

the only way to make a comment in rust is with `//`

## Control Flow

Control flow: the ability to run code conditionally

### `if` Expressions

```rust
fn main() {
  let number = 3;

  if number < 5 {
    println!("Condition is true");
  } else {
    println!("Condition is false");
  }
}
```

#### `else if`

```rust
fn main() {
    let number = 6;

    if number % 4 == 0 {
        println!("number is divisible by 4");
    } else if number % 3 == 0 {
        println!("number is divisible by 3");
    } else if number % 2 == 0 {
        println!("number is divisible by 2");
    } else {
        println!("number is not divisible by 4, 3, or 2");
    }
}
```

#### Using `if` inside `let`

```rust
fn main() {
    let condition = true;
    let number = if condition { 5 } else { 6 };

    println!("The value of number is: {number}");
}
```

if the types are mismatched inside the `let` statement, an error will be thrown

### Repetition with Loops

Rust has three kinds of loops:

1. `loop`
2. `while`
3. `for`

#### Repetition with `loop`

This keyword loops over a block of code forever or until it is told explicitly to stop.

```rust
fn main() {
  loop {
    println!("again!");
  }
}
```

This will run infinitely until the user presses `^C`. this loop can be broken out of programmatically with the `break` keyword.

##### Returning Values from Loops

One of the uses of a loop is to retry some block of code until a specific line runs:

```rust
fn main() {
    let mut counter = 0;

    let result = loop {
        counter += 1;

        if counter == 10 {
            break counter * 2;
        }
    };

    println!("The result is {result}");
}
```

##### Loop Labels

when using multiple nested loops, loos labels can be used to specify which loop to `break` or `continue`.

```rust
fn main() {
    let mut count = 0;
    'counting_up: loop {
        println!("count = {count}");
        let mut remaining = 10;

        loop {
            println!("remaining = {remaining}");
            if remaining == 9 {
                break;
            }
            if count == 2 {
                break 'counting_up;
            }
            remaining -= 1;
        }

        count += 1;
    }
    println!("End count = {count}");
}
```

#### Repetition with `while`

while loops continue as long as a value is true.

```rust
fn main() {
    let mut number = 3;

    while number != 0 {
        println!("{number}!");

        number -= 1;
    }

    println!("LIFTOFF!!!");
}
```

#### Repetition with `for`

You can use the while loop to loop over an array, but a for loop is much better:

```rust
fn main() {
    let a = [10, 20, 30, 40, 50];

    for element in a {
        println!("the value is: {element}");
    }
}
```
