---
id: Writing Tests
aliases:
  - Writing Tests
tags:
---

# Writing Tests

Tests are functions that verify that the non-test code is functioning in the expected manner

there are three main parts to a test:

1. Set up any needed data or state
2. Run the code you want to test
3. Assert the results are what you expect

Asserting results just means making sure the expecteed result was returned.

functions that are used in tests must be annotated with `#[test]`

```rust
#[cfg(test)]
mod tests {
    #[test]
    fn it_works() {
      let result = 2+2;
    assert_eq!(result, 4);
  }
}
```

this is the basic structure of a test, the following are some more basic examples of different syntax and such

```rust
    #[test]
    fn greeting_contains_name() {
        let result = greeting("Carol");
        assert!(
            result.contains("Carol"),
            "Greeting did not contain name, value was `{}`",
            result
        );
    }
```

Custom test failure msg

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
}

#[cfg(test)]
mod tests {
    use super::*;

    #[test]
    #[should_panic]
    fn greater_than_100() {
        Guess::new(200);
    }
}
```

testing a function that should panic.

```rust
// --snip--

impl Guess {
    pub fn new(value: i32) -> Guess {
        if value < 1 {
            panic!(
                "Guess value must be greater than or equal to 1, got {}.",
                value
            );
        } else if value > 100 {
            panic!(
                "Guess value must be less than or equal to 100, got {}.",
                value
            );
        }

        Guess { value }
    }
}

#[cfg(test)]
mod tests {
    use super::*;

    #[test]
    #[should_panic(expected = "less than or equal to 100")]
    fn greater_than_100() {
        Guess::new(200);
    }
}
```

should_panic with expected msg

## Using Result<T, E> in tests

```rust
#[cfg(test)]
mod tests {
    #[test]
    fn it_works() -> Result<(), String> {
        if 2 + 2 == 4 {
            Ok(())
        } else {
            Err(String::from("two plus two does not equal four"))
        }
    }
}
```

this is good for tests that check multiple factors that could error.

# Controlling How Tests Are Run

`cargo test --help` for all options

`cargo test -- --help` for options that can be passed to the test binary

# Test Organization

As usual, tests are seperated into unit tests and integration tests.

## Unit Tests

the purpose of these is to test peieces of code in isolation, this is put in the src dir in each file with the tested code, the accepted method is to use a module named `test` and the annotate each test function with `cfg(test)`

in Rust, although a functino coudl be private and defined outside of the `tests` module, it can still be tested in the same file.

## integration tests

these are located in the tests directory, each file in this directory is compiled as a seperate crate, so they cannot access private functions in the library crate.

they are external to the library, so they use it in the same way any other code would, the main purpouse is to test whether or not parts of your library work together to gibe a specific functionality.

the way they can be used is by imported the library into the file and then writing the test:

```rust
use adder;

#[test]
fn it_adds_two() {
    assert_eq!(4, adder::add_two(2));
}
```

These files only get compiled with `cargo test` and ar eleft out of the binary in any other situation.

