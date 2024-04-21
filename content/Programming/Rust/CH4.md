---
id: ch4
aliases:
  - CH4|
tags: []
---


# CH4-Ownership

Ownership is a set of rules that govern how Rust manages memory

## The Stack and the Heap

The stack orders values in the order it gets them and removes them in the opposite order, AKA Last in First out.

The heap is memory allocation, meaning that when putting data on the heap, you are given a pointer which is the memory address of that data.
Because the pointer is fixed length, it can be stored on the stack, but as soon as you need the data you have to go to the heap.

> Accessing data on the heap is slower than the stack because you have to follow a pointer to get there.

## Ownership Rules

- Each value in Rust has an owner.
- There can only be one owner at a time.
- When the owner goes out of scope, the value is dropped.

## Variable Scope

A scope is the range within a program for which an item is valid.

```rust
{
  let s = "hello";

  // do things with s

}

println!("{s}") // Error: s has been put out of scope
```

## The `String` Type

Up until now, we've only used string literals, immutable variables that are stored on the stack, the `String` type is stored on the heap and can be mutable:

```rust
let s = String::from("hello")
```

> `::` refers to a namespace, so in this case, get the `from` function that is part of the `String` namespace.

updating the code to allow for mutability:

```rust
let mut s = String::from("hello");

s.push_str(", world!"); // push_str() takes a string literal and adds it to the String

println!("{}", s); // hello, world!
```

### Memory and Allocation

With a sting literal, it can be stored on the stack as the size is immutable and know at compile time. but with a `String` the size and contents can change throughout the program so it is impossible to hardcode.

In that case, we know:

- The memory must be requested from `malloc` at runtime
- The memory that is allocated must be returned when the `String` goes out of scope

`String::from()` can request the memory it needs, not too complicated
Rust is unique when it comes to reallocateing the memory back, usually there is a garbage collector(GC) that keeps track of and cleans up memory that is unused, this works, however the rate and interval at which the memory is deallocated is unkown.

Usually, when there is no GC, it is up to the user to clean up memory. Where Rust shines is it takes the best of both extremes with ownership. When the variable goes out of scope, the memory is reallocated.

this is really simple with one variable, but there are cases where it gets complex:

```rust
let x = 5;
let y = x;
```

While at first glance it seems as if `let y = 5` would do the same. in this case it does because both variables are on the stack.

```rust
let s1 = String::from("hello");
let s2 = s1;
```

This is about the same, so it might be assumed that the value of s1 will be copied into s2, keeping both variables in scope. but this isn't true.

As explained previously, the `String` is on the heap, and data on the heap is addresed by a pointer on the stack:

![Rust_StringHeap.png](Rust_StringHeap.png)

This represents what `s1` is, a pointer on the stack to a string of data on the heap.

![Rust_PointerCopy.png](Rust_PointerCopy.png)

this is actually what is happening when `s2 = s1` is called, they are set to the same pointer, not a copy of the data on the heap.

This is great, less data has to be copied over to represent the same value, so it utilizes the effeciency of the stack, while still keeping mutability and size variance. The problem arises however, when the variables go out of scope. When `s1` goes out of scope it will drop the data at the pointer.

This leads to `s2` being a pointer to empty memory, and when `s2` is dropped, all hell breaks loose. This is a double free error.

To combat this, Rust considers `s1` as invalid after the pointer gets copied to `s2`, AKA out of scope, but the data isn't dropped.

![Rust_DropDouble.png](Rust_DropDouble.png)

## `clone`

If you do need a 'deep' copy of a `String`, not just the pointer, this is a method referred to as `clone`.

```rust
let s1 = String::from("hello");
let s2 = s1.clone(); // not just the pointer, but the heap too :)
```

In the example above, printing both variables would be valid, as they are both different places on the heap and different pointers, more like this:

![Rust_IndVars.png](Rust_IndVars.png)

This method can be expensive, so be careful.

## Stack Only Data

In the example with two immutable variables that are stored on the stack, there is no difference between a shallow and deep copy, as Rust sees they are both on the stack and can just create the data again on the stack.

This also doesn't take the 1st var out of scope.

This behavior is made possible with the `Copy` trait.

Here are some of the types that implement Copy:

- All the integer types, such as u32.
- The Boolean type, bool, with values true and false.
- All the floating-point types, such as f64.
- The character type, char.
- Tuples, if they only contain types that also implement Copy. For example, (i32, i32) implements Copy, but (i32, String) does not.

## Ownership and Functions

When passing args to a function, those variabeles get passed and the owner becomes the function, thus moving the variables out of scope.

```rust
fn main() {
    let s = String::from("hello");  // s comes into scope

    takes_ownership(s);             // s's value moves into the function...
                                    // ... and so is no longer valid here

    let x = 5;                      // x comes into scope

    makes_copy(x);                  // x would move into the function,
                                    // but i32 is Copy, so it's okay to still
                                    // use x afterward

} // Here, x goes out of scope, then s. But because s's value was moved, nothing
  // special happens.

fn takes_ownership(some_string: String) { // some_string comes into scope
    println!("{}", some_string);
} // Here, some_string goes out of scope and `drop` is called. The backing
  // memory is freed.

fn makes_copy(some_integer: i32) { // some_integer comes into scope
    println!("{}", some_integer);
} // Here, some_integer goes out of scope. Nothing special happens.
```

## Return Values and Scope

Extending the logic, when returning values out of a function, the ownership is also transfered.

```rust
fn main() {
    let s1 = gives_ownership();         // gives_ownership moves its return
                                        // value into s1

    let s2 = String::from("hello");     // s2 comes into scope

    let s3 = takes_and_gives_back(s2);  // s2 is moved into
                                        // takes_and_gives_back, which also
                                        // moves its return value into s3
} // Here, s3 goes out of scope and is dropped. s2 was moved, so nothing
  // happens. s1 goes out of scope and is dropped.

fn gives_ownership() -> String {             // gives_ownership will move its
                                             // return value into the function
                                             // that calls it

    let some_string = String::from("yours"); // some_string comes into scope

    some_string                              // some_string is returned and
                                             // moves out to the calling
                                             // function
}

// This function takes a String and returns one
fn takes_and_gives_back(a_string: String) -> String { // a_string comes into
                                                      // scope

    a_string  // a_string is returned and moves out to the calling function
}
```

# References and Borrowing

Instead of taking ownership of a variable, you can pass a reference to functions, a reference is like a pointer, an address specifying where the data is, the data is owned by some other variable and the reference address is guarenteed to point to a valid value of a valid type.

```rust
fn main() {
    let s1 = String::from("hello");

    let len = calculate_length(&s1);

    println!("The length of '{}' is {}.", s1, len);
}

fn calculate_length(s: &String) -> usize {
    s.len()
}
```

This example doesn't take `s1` out of scope, it just passes a reference of it to `calculate_length`.

![Rust_Ref.png](Rust_Ref.png)

> There is also a concept called dereferencing, using the `*` operator.

Another point to realize is that the function no longer takes in a type of `String`, but rather a reference to it.

References are immutable by default, so they cannot be changed.

## Mutable References

```rust
fn main() {
  let mut s = String::from("hello");

  change(&mut s);
}

fn change(some_string: &mut String) {
  some_string.push_str(", world");
}
```

This is valid because of the `mut` keyword when passing in the arg to `change`. This also has to be changed in the function signature.

There is a restriction on mutable references, no other references can be made while that reference is within scope. This promotes memory saftey as you won't be able to change a value twice at the same time.

This is known as a Data Race error

```rust
    let mut s = String::from("hello");

    let r1 = &s; // no problem
    let r2 = &s; // no problem
    println!("{} and {}", r1, r2);
    // variables r1 and r2 will not be used after this point

    let r3 = &mut s; // no problem
    println!("{}", r3);
```

This is valid because while the mutable reference is in scope, there are no other references made.

## Dangling References

With pointers comes dangling: referencing a location in memory that has been given to someone else. In Rust, becuase of the ownership rules, this cannot happen because when the data goes out of scope, it is only because the pointer that owns it went out of scope.

The most common way this happens is returning a reference to a value in a function when the function is just about to leave the scope, leaving a dangling reference. The Rust compiler will throw an error when you do this.

# The Slice Type

A slice is reference to a contiguous sequence of elements

> Ex. Problem: Write a function that inputs a sting of words seperated by spaces and returns the first word that is in that string, if there are no spaces, the whole string should be returned.

```rust
fn first_word(s: &String) -> usize {
    let bytes = s.as_bytes();

    for (i, &item) in bytes.iter().enumerate() {
        if item == b' ' {
            return i;
        }
    }

    s.len()
}
```

the `as_bytes` method will return an array of bytes.
then, using the `iter` method along with `enumerate` you can go through each letter in the string while keeping track of the index.

if nothing is found in the loop, it returns `s.len`

Because the returned `usize` is not correlated in any way with `&String`, there is no guarantee that they both exit the scope at the same time. Consider the following:

```rust
fn main() {
    let mut s = String::from("hello world");

    let word = first_word(&s); // word will get the value 5

    s.clear(); // this empties the String, making it equal to ""

    // word still has the value 5 here, but there's no more string that
    // we could meaningfully use the value 5 with. word is now totally invalid!
}
```

## String Slices

A string slice is a reference to a part of a `String`:

```rust
let s = String::from("hello world!");

let hello = &s[0..5];
let world = &s[6..11];
```

When a string slice is made, the variable on the stack is a pointer to the starting index, and the len is how far away the ending index is

![StringSliceRust.png](assets/imgs/StringSliceRust.png)

With the `..` syntax, if the index is at 0 you can drop the value before the periods, same with the end.

```rust
let hello = &s[..5];
let world = &s[6..];
```

So, to wrap back to the problem, the `first_word` function is more like this:

```rust
fn first_word(s: &String) -> &str {
  let bytes = s.as_bytes();

    for (i, &item) in bytes.iter().enumerate() {
        if item == b' ' {
            return &s[0..i];
        }
    }

    &s[..]
}
```

So instead of returning an index, it returns a reference back to the original string.

## Using String Literals as Slices and function params

a literal string is of type `&str`, an immutable reference, knowing this we can improve the solution just a bit:

```rust
fn main() {
    let my_string = String::from("hello world");

    // `first_word` works on slices of `String`s, whether partial or whole
    let word = first_word(&my_string[0..6]);
    let word = first_word(&my_string[..]);
    // `first_word` also works on references to `String`s, which are equivalent
    // to whole slices of `String`s
    let word = first_word(&my_string);

    let my_string_literal = "hello world";

    // `first_word` works on slices of string literals, whether partial or whole
    let word = first_word(&my_string_literal[0..6]);
    let word = first_word(&my_string_literal[..]);

    // Because string literals *are* string slices already,
    // this works too, without the slice syntax!
    let word = first_word(my_string_literal);
}
```

## Other types of slices

Slicing is not just for strings, you can also use it with other types:

```rust
let a = [1, 2, 3, 4, 5];

let slice = &a[1..3];

assert_eq!(slice, &[2, 3]);
```

