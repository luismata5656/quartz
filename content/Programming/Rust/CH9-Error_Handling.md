---
id: CH9-Error_Handling
aliases:
  - CH9-Error_Handling
tags: []
---

# CH9-Error_Handling

Rust groups errors into _recoverable_ and _unrecoverable_ categories. For a recoverable error, such as a file not found error, it’s reasonable to report the problem to the user and retry the operation. Unrecoverable errors are always symptoms of bugs, like trying to access a location beyond the end of an array.

Rust has the type `Result<T, E>` for recoverable errors and `panic!` macro is like a segfault for unrecoverables.

# Unrecoverable Errors with `panic!`

With the `panic!` macro, Rust stops execution and prints a failure message. This is similar to `assert!` macro, but `panic!` can be used in production code.

> When panicing, Rust will walk back up the stack and clean up the data, this is expensive and can be circumvented by just aborting, though this memory will now be in memory still, or at least until somewthing writes over it.
> to abot, use `panic = 'abort'` in Cargo.toml

```rust
fn main() {}
  let v  = vec![1, 2, 3];

  v[99]; // PANIC!
}
```

attempting to get a value from a vector at an index that doesn’t exist will cause Rust to panic and exit the program.

In C this works, but is a massive vulnerability.

# Recoverable Errors with `Result`

the `Result<T, E>` enum has two variants:

```rust
enum Result<T, E> {
  Ok(T),
  Err(E),
}
```

here is an example of using `Result` to open a file:

```rust
use std::fs::File;

fn main() {
    let greeting_file_result = File::open("hello.txt");

    let greeting_file = match greeting_file_result {
      Ok(file) => file,
      Err(error) => match error.kind() {
        ErrorKind::NotFound => match File::create("hello.txt") {
          Ok(fc) => fc,
          Err(e) => panic!("Problem creating the file: {:?}", e),
        },
        other_error => panic!("Problem opening the file: {:?}", other_error),
      },
    };
}
```

This will create a file if it not found, any other error will panic.

## Shortcuts for Panic on Error: `unwrap` and `expect`

```rust
use std::fs::File;

fn main() {
  let f = File::open("hello.txt").unwrap();
}
```

This will panic if the file is not found.

```rust
use std::fs::File;

fn main() {
  let f = File::open("hello.txt").expect("Failed to open hello.txt");
}
```

this will panic with the message provided.

## Propagating Errors

```rust
use std::fs::File;
use std::io::{self, Read};

fn read_username_from_file() -> Result<String, io::Error> {
    let username_file_result = File::open("hello.txt");

    let mut username_file = match username_file_result {
        Ok(file) => file,
        Err(e) => return Err(e),
    };

    let mut username = String::new();

    match username_file.read_to_string(&mut username) {
        Ok(_) => Ok(username),
        Err(e) => Err(e),
    }
}
```

When you propogate, you give the program a higher chance of completing, as when an error occurs, it can just pass it over, and hopefully everything works out :)

### The ? Operator

```rust
use std::fs::File;
use std::io::{self, Read};

fn read_username_from_file() -> Result<String, io::Error> {
    let mut username_file = File::open("hello.txt")?;
    let mut username = String::new();
    username_file.read_to_string(&mut username)?;
    Ok(username)
}
```

This is a shorthand way of propogating.

This operator can only be use in function with a return type that is compatible with the value that the `?` is used on, this is because when `?` escapes the call, it will return the value inside of the `Ok` variant of the `Result` enum.

# Deciding How to Handle Errors

Production code should take into account every possible error and handle it, but this is not always possible, and sometimes it is not worth it.

in examples, prototypes, and test, it is fine to use `unwrap` and `expect` as they will panic if an error occurs, and this is fine for testing.

## Knowing more than the compiler, that which makes you human.

There are certain cases when basic logic will show that a peice of code cannot ever fail, be careful doing this as it introduces human stupidity. An easy example is when there is a hardcode string in memory, unless there is a catastrophic system failure(Wherein you have a different problem entirely). THat string will always be where you need it.

It is advised to panic when the control flow has been broken in an unrecoverable way, so the code will end up in a 'bad' or _unsafe_ state.

## Creating Custom Types for Validation

```rust
pub struct Guess {
    value: i32,
}

impl Guess {
    pub fn new(value: i32) -> Guess {
        if value < 1 || value > 100 {
            panic!("Guess value must be between 1 and 100, got {}.", value);
        }

        Guess { value }
    }

    pub fn value(&self) -> i32 {
        self.value
    }
}
```

Using custom structs with methods can clean up code a bit.
