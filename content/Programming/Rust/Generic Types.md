---
id: "2024-01-06"
aliases:
  - CH10-Generic_Types.md
  - CH10-Generic_Types
tags: []
draft: true
---

# CH10-Generic_Types.md

abstracting over types with generic parameters

generic types are abstract stand-ins for concrete types or other properties

they can define top level interaction behavior between other generics without needing to know what is in their place at compile time.

Functions can take in generics, and structs can be generic.

Some example of generics already used are `Vec<T>` and `HashMap<K, V>`

these are from [Chapter 8](Programming/Rust/CH8.md#Common_Collections)

## Removing Duplication by Extracting a Function

```rust
fn main() {
    let number_list = vec![34, 50, 25, 100, 65];

    let mut largest = &number_list[0];

    for number in &number_list {
        if number > largest {
            largest = number;
        }
    }

    println!("The largest number is {}", largest);
}
```

This code works, but we have to duplicate code if you want to use a second array, that is why functions like this are often abstracted out

```rust
fn largest(list: &[i32]) -> &i32 {
    let mut largest = &list[0];

    for item in list {
        if item > largest {
            largest = item;
        }
    }

    largest
}

fn main() {
    let number_list = vec![34, 50, 25, 100, 65];

    let result = largest(&number_list);
    println!("The largest number is {}", result);

    let number_list = vec![102, 34, 6000, 89, 54, 2, 43, 8];

    let result = largest(&number_list);
    println!("The largest number is {}", result);
}
```

# Generic data types

when using generic data types in functions, they take place of the paramaters and return values, doing this allows for more flexibility and eventually leads into monaads.

Continuing with the previous example, we can make the function generic over any type that implements the `PartialOrd` and `Copy` traits:

```rust
fn largest<T: PartialOrd + Copy>(list: &[T]) -> T {
    let mut largest = list[0];
    for &item in list {
        if item > largest {
            largest = item;
        }
    }
    largest
}
```

## Using `struct` Generics

```rust
struct Point<T> {
    x: T,
    y: T,
}

fn main() {
    let integer = Point { x: 5, y: 10 };
    let float = Point { x: 1.0, y: 4.0 };
}
```

since there is only one type: `T`, both x and y are the same type.

## Enum Generics

```rust
enum Option<T> {
    Some(T),
    None,
}
```

pretty self explanatory

## Method Definitions

```rust
struct Point<T> {
    x: T,
    y: T,
}

impl<T> Point<T> {
    fn x(&self) -> &T {
        &self.x
    }
}

fn main() {
    let p = Point { x: 5, y: 10 };

    println!("p.x = {}", p.x());
}
```

This is useful, but sometimes you want to implement methods only on certain instances of a generic type, for example, you may want to implement methods on `Point<f32>` but not on `Point<T>`.

```rust
impl Point<f32> {
    fn distance_from_origin(&self) -> f32 {
        (self.x.powi(2) + self.y.powi(2)).sqrt()
    }
}
```

when rust compiles generics, it can do monomorphization, this is when the compile will read the values inside of `Option<T>` instances and in the following case, it finds two cases, it will then expand the generic definition of `Option` into two definitions specialzed for the cases, so there is no overhead runtime cost for using generics in our code.

```rust
let integer = Some(5);
let float = Some(5.0);
```

# Traits

a trait is a shared behavior, an abstract high level behavior. this is often called an _interface_ in other langs.

## `trait` Definition

```rust
pub trait Summary {
    fn summarize(&self) -> String;
}
```

This defines a trait called `Summary` that has one method, `summarize`, that takes `self` and returns a `String`.

```rust
pub struct NewsArticle {
    pub headline: String,
    pub location: String,
    pub author: String,
    pub content: String,
}

impl Summary for NewsArticle {
    fn summarize(&self) -> String {
        format!("{}, by {} ({})", self.headline, self.author, self.location)
    }
}

pub struct Tweet {
    pub username: String,
    pub content: String,
    pub reply: bool,
    pub retweet: bool,
}

impl Summary for Tweet {
    fn summarize(&self) -> String {
        format!("{}: {}", self.username, self.content)
    }
}
```

## Default Implementations

```rust
pub trait Summary {
    fn summarize(&self) -> String {
        String::from("(Read more...)")
    }
}
```

a default behvior can be defined for a trait, and then overriden in a specific implementation of that trait.

## Traits as Parameters

```rust
pub fn notify(item: &impl Summary) {
    println!("Breaking news! {}", item.summarize());
}
```

this takes in any type that implements the `Summary` trait

## Trait Bounds

```rust
pub fn notify<T: Summary>(item: &T) {
    println!("Breaking news! {}", item.summarize());
}
```

this is the same as the previous example, but with a different syntax

the trait bound syntax can give more information to the compiler, for example, if we wanted to take two parameters that implement the same trait, we could do this:

```rust
pub fn notify<T: Summary>(item1: &T, item2: &T) {
    // ...
}
```

## `where` Clauses for Method Parameters

```rust
fn some_function<T, U>(t: &T, u: &U) -> i32
where
    T: Display + Clone,
    U: Clone + Debug,
{
}
```

This syntax makes the code more readable if you have a lot of different traits that are needed as args.

## Using trait bounds to conditionally implement methods

```rust
use std::fmt::Display;

struct Pair<T> {
    x: T,
    y: T,
}

impl<T> Pair<T> {
    fn new(x: T, y: T) -> Self {
        Self { x, y }
    }
}

impl<T: Display + PartialOrd> Pair<T> {
    fn cmp_display(&self) {
        if self.x >= self.y {
            println!("The largest member is x = {}", self.x);
        } else {
            println!("The largest member is y = {}", self.y);
        }
    }
}
```

This will only implement `cmp_display` if `T` is a type that implements PartialOrd and Display, this is good because it guarentees that any type put through pair will be given the ability to be printeed if it can be.

# Validating References with Lifetimes

Lifetimes are a generic, they ensure that references are valid as long as we need them to be.

every reference has a _lifetime_

## Preventing Dangling References with Lifetimes

```rust
{
    let r;
    {
        let x = 5;
        r = &x;
    }
    println!("r: {}", r);
}
```

This throws an error as `x` is out of scope when we try to use `r`, even though `r` is still valid, `x` has fallen out of scope, and since the data at `r` is a reference to the data at `x`, this would be a dangling refernce, instead Rust just throws an error, which is better.

### Borrow Checker

removing the dangling reference error is the job of the borrow checker, it compares scopes to determine if all borrows are valid.

```rust
{
    let r;                // ---------+-- 'a
                          //          |
    {                     //          |
        let x = 5;        // -+-- 'b  |
        r = &x;           //  |       |
    }                     // -+       |
                          //          |
    println!("r: {}", r); //          |
}                         // ---------+
```

```rust
{
    let x = 5;            // ----------+-- 'b
                          //           |
    let r = &x;           // --+-- 'a  |
                          //   |       |
    println!("r: {}", r); //   |       |
                          // --+       |
}                         // ----------+
```

## Lifetime Syntax

```rust
fn longest<'a>(x: &'a str, y: &'a str) -> &'a str {
    if x.len() > y.len() {
        x
    } else {
        y
    }
}
```

The above code uses lifetime annotions in the function signature, this tells the compiler that the returned reference will live at least as long as the shorter of the two lifetimes.

```rust
fn main() {
    let string1 = String::from("long string is long");

    {
        let string2 = String::from("xyz");
        let result = longest(string1.as_str(), string2.as_str());
        println!("The longest string is {}", result);
    }
}
```

Above is valid code, below is an error because `string2` has now fallen out of scope, even though the data inside is obviously going to be shorter, it is safer to throw an error.

```rust
fn main() {
    let string1 = String::from("long string is long");
    let result;
    {
        let string2 = String::from("xyz");
        result = longest(string1.as_str(), string2.as_str());
    }
    println!("The longest string is {}", result);
}
```

## Elision Rules

There are specific cases in functions that the lifetime definitions are not required, these rules are hard coded into Rust, and they are called the Elision Rules:

1 Any parameter that is a reference is given a lifetime:

```rust
fn foo<'a>(x: &'a i32) {
```

Becomes

```rust
fn foo(x: &i32) {
```

2 if there is exactly one input lifetime parameter, that lifetime is assigned to al output lifetime paramets:

```rust
fn foo<'a>(x: &'a i32) -> &'a i32 {
```

3 if there is multiple input lifetime parameters, but one of them is `&self` or `&mut self`, the lifetime of `self` is assigned to all output lifetime parameters

# Generic Types, Traits, and Lifetimes Together

```rust
use std::fmt::Display;

fn longest_with_an_announcement<'a, T>(
    x: &'a str,
    y: &'a str,
    ann: T,
) -> &'a str
where
    T: Display,
{
    println!("Announcement! {}", ann);
    if x.len() > y.len() {
        x
    } else {
        y
    }
}
```
