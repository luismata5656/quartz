---
id: CH6-Enums
aliases:
  - CH6-Enums
tags: []
draft: true
---

# CH6-Enums

Enums allow you to define a type by enumerating it's _variants_

# Defining an Enum

Enums are a way of saying a value is one of a possible set.

Like with the Rectangle case from [Chapter 5](/Programming/Rust/CH5.md#Using Structs to Structure Related Data) the Rectangle is one of a set of shapes such as Circle, Triangle, etc.

> Say we need to work with IPs, both v4 and v6. since there are only two possible values, an enum can be used, because depending on the type of ip it is, it holds different data but it is still fundamentally an IP.

```rust
enum IpAddrKind {
  V4,
  V6,
}
```

These are instanciaed like so:

```rust
let four = IpAddrKind::V4;
let six = IpAddrKind::V6;
```

The enum types are namespaced under the identifier, they are still the same type though, so functions that deal with IPs can still deal with both:

```rust
fn route(ip_kind: IpAddrKind) {}
```

Both variants are of the same type, so they can be used interchangably.
each of these variants can have data associated with them, like so:

```rust
enum IpAddr {
  V4(String),
  V6(String),
}

let home = IpAddr::V4(String::from("127.0.0.1"));
let loopback = IpAddr::V6(String::from("::1"));
```

These variants can also have different types and amounts in them:

```rust
enum IpAddr {
  V4(u8, u8, u8, u8),
  V6(String),
}

let home = IpAddr::V4(127, 0, 0, 1);
let loopback = IpAddr::V6(String::from("::1"));
```

This IP example is already defined in the standard library, but they implement it as such:

```rust
struct Ipv4Addr {
  // --snip--
}

struct Ipv6Addr {
  // --snip--
}

enum IpAddr {
  V4(Ipv4Addr),
  V6(Ipv6Addr),
}
```

So any data can be placed within the enum, even other enum.

```rust
enum Message {
  Quit,
  Move { x: i32, y: i32 },
  Write(String),
  ChangeColor(i32, i32, i32),
}
```

This enum can be used like so:

```rust
impl Message {
  fn call(&self) {
    // method body would be defined here
  }
}

let m = Message::Write(String::from("hello"));
m.call();
```

## The Option Enum

As it is often used in many places, the Option enum is included in the standard library, it looks like this:

```rust
enum Option<T> {
  Some(T),
  None,
}
```

> null references were my billion dollar mistake - Tony Hoare

# The match Control Flow Operator

the `match` operator is like a `switch` statement in other languages, but it is more powerful, and is used more often.

```rust
enum Coin {
  Penny,
  Nickel,
  Dime,
  Quarter,
}

fn value_in_cents(c: Coin) -> u8 {
  match c {
    Coin::Penny => 1,
    Coin::Nickel => 5,
    Coin::Dime => 10,
    Coin::Quarter => 25,
  }
}
```

## Patterns that Bind to Values

```rust
#[derive(Debug)]
enum UsState {
  Alabama,
  Alaska,
  // --snip--
}

enum Coin {}
  Penny,
  Nickel,
  Dime,
  Quarter(UsState),
}
```

so now each variant still works but when using the Quarter variant, it can be used like so:

```rust
fn value_in_cents (coin: Coin) -> u8 {
  match coin {
    Coin::Quarter(state) => {
      println!("State quarter from {:?}!", state);
      25
    },
    // --snip--
  }
}
```

Match statements must be exhaustive, so all possible values must be accounted for, so a catch all can be used:

```rust
let dice_roll = 7;
match dce_roll {
  3 => println!("three"),
  4 => println!("four"),
  6 => println!("six"),
  _ => println!("not a valid roll"),
}
```

`other` can also be used instead of `_` but it is less clear.

# Concise Control Flow with if let

when using the `Option` type, the `match` operator is often used, but there is a more concise way of doing this with `if let`:

```rust
let config = Some(3u8);
if let Some(3) = some_u8_value {
  println!("three");
}
```
