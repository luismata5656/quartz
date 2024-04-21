---
id: ch5
aliases:
  - Using Structs to Structure Related Data
tags: []
draft: true
---

# Using Structs to Structure Related Data

a struct is a custom data type that holds multiple values of different types.

# Defining and Instantiating Structs

in a struct, each piece of data is named, they are defined with the `struct` keyword

```rust
struct User {
  active: bool,
  username: String,
  email: String,
  sign_in_count: u64.
}
```

In order to use the struct, an instance of it must be created, they are instantiated as such:

```rust
fn main() {
  let user1 = User {
    active: true,
    username: String::from("someusername123"),
    email: String::from("someone@example.com"),
    sign_in_count: 1,
  }

  println!("{}", user1.email)
}
```

Specific values in a struct cannot be mutable, if the struct nneds to change, it can be made mutable durin ginstantiation.

```rust
fn build_user(email: String, username: String) -> User {
    User {
        active: true,
        username: username,
        email: email,
        sign_in_count: 1,
    }
}
```

## Using the Field Init Shorthand

There is a shorthand for the above init function, since the field names are the same as the params, you can write the function like so:

```rust
fn build_user(email: String, username: String) -> User {
    User {
        active: true,
        username,
        email,
        sign_in_count: 1,
    }
}
```

## Creating Instances from Other Instances with Struct Updates

The struct update syntax allows for you to create a new instance of a struct that includes most of the values from another instance, but change some.

Continuing the above function:

```rust
fn main() {
    // --snip--

    let user2 = User {
        active: user1.active,
        username: user1.username,
        email: String::from("another@example.com"),
        sign_in_count: user1.sign_in_count,
    };
}
```

Struct update syntax allows us to use `..` to have the same effect:

```rust
fn main() {
  // --snip--

  let user2 = User {
    email: String::from("another@example.com"),
    ..user1
  };
}
```

## Structs without named fields

```rust
struct Color(i32, i32, i32);
struct Point(i32, i32, i32);

fn main() {
    let black = Color(0, 0, 0);
    let origin = Point(0, 0, 0);
}
```

## Unit-Like Structs

```rust
struct AlwaysEqual;

fn main() {
    let subject = AlwaysEqual;
}
```

a struct without any fields is a unit-like struct. these can be useful whe you need to implement a trait on a type but don't have any data that needs to be stored in the type.

# Method Syntax

methods, like functions, use the `fn` keyword, they can have params and a return value. Methods are defined within a Struct, enum, or trait object. the first param is always self.

```rust
#[derive(Debug)]
struct Rectangle {
    width: u32,
    height: u32,
}

impl Rectangle {
    fn area(&self) -> u32 {
        self.width * self.height
    }
}

fn main() {
    let rect1 = Rectangle {
        width: 30,
        height: 50,
    };

    println!(
        "The area of the rectangle is {} square pixels.",
        rect1.area()
    );
}
```

You can also define a method as a name of one the attributes of the struct:

```rust
impl Rectangle {
  fn width(&self) -> bool {
    self.width > 0
  }
}

fn main() {
  let rect1 = Rectangle {
    width: 30,
    height: 50,
  };
  if rect1.width() {
    println!("The width is greater than 0, it is {}", rect1.width);
  }
}
```

usually when we give a method the same name as a field it should just return the value in the field and nothing else, these are called getters, Rust doesn't implement them automatically, so we have to do so manually.

the next method to implement is a `can_hold` method, to check whether another object of type rectangle can fit inside the rectangle:

```rust
impl Rectangle {
  fn can_hold(&self, other: &Rectangle) -> bool {
    self.width > other.width && self.height > other.height
  }
}

fn main() {
    let rect1 = Rectangle {
        width: 30,
        height: 50,
    };
    let rect2 = Rectangle {
        width: 10,
        height: 40,
    };
    let rect3 = Rectangle {
        width: 60,
        height: 45,
    };

    println!("Can rect1 hold rect2? {}", rect1.can_hold(&rect2));
    println!("Can rect1 hold rect3? {}", rect1.can_hold(&rect3));
}
```

## Associated Functions

methods that don't take `self` as a param are called associated functions, they are associated with the struct, they are often used as constructors that will return a new instance of the struct.

```rust
impl Rectangle {
  fn square(size: u32) -> Rectangle {
    Rectangle {
      width: size,
      height: size,
    }
  }
}
```

this will return a square with the given size.

These are called as such:

```rust
let sq = Rectangle::square(3);
```

## Multiple `impl` Blocks

A single struct can have several `impl` blocks, each block is still in scope for the entire struct.

```rust
impl Rectangle {
    fn area(&self) -> u32 {
        self.width * self.height
    }
}

impl Rectangle {
    fn can_hold(&self, other: &Rectangle) -> bool {
        self.width > other.width && self.height > other.height
    }
}
```

There is no reason to separate these, but it is possible.
