---
id: CH8
aliases: []
tags: []
---

# Common_Collections

In the standard library, there are a few collections that are used often, they are:

- Vectors
- Strings
- Hash Maps

# Storing Lists of Values with Vectors

`Vec<T>` is a growable array type, it is allocated on the heap, and can store any type.

## Creating a New Vector

```rust
let mut v: Vec<i32> = Vec::new();
let v1 = vec![1, 2, 3];
```

To add values to a vector, the `push` method can be used:

```rust
v.push(5);
```

## Reading Elements of Vectors

```rust
    let v = vec![1, 2, 3, 4, 5];

    let third: &i32 = &v[2];
    println!("The third element is {third}");

    let third: Option<&i32> = v.get(2);
    match third {
        Some(third) => println!("The third element is {third}"),
        None => println!("There is no third element."),
    }

```

Where Vectors can get tricky is if you are holding an immutable reference to some value and then you try to push or change the vector in some way, although you may not change the reference, it is still invalid

## Iterating through Vectors

```rust
    let v = vec![100, 32, 57];
    for i in &v {
        println!("{}", i);
    }
```

## Using an Enum to Store Multiple Types

```rust
    enum SpreadsheetCell {
        Int(i32),
        Float(f64),
        Text(String),
    }

    let row = vec![
        SpreadsheetCell::Int(3),
        SpreadsheetCell::Text(String::from("blue")),
        SpreadsheetCell::Float(10.12),
    ];
```

# Storing UTF-8 Encoded Text with Strings

Up until now, strings have been defined in the following ways:

- `&str`: string slices
- `String`: growable, heap-allocated data structure
- `str`: primitive type
- `&String`: string slice

Like a Vector, a String is a wrapper over a `Vec<u8>`. and we can use `push_str` and `push` to append a string slice to any `String`.

# Hash Maps

At a high level, Hash Maps are a table that maps a set of keys type `k` to type `v`using a hashing function, the keys are unique, and the values can be duplicated.

Basic Usage of Hsh Maps:

```rust
use std::collections::HashMap;

let mut scores = HashMap::new();

scores.insert(String::from("Blue"), 10);
scores.insert(String::from("Yellow"), 50);

for (key, value) in &scores {
    println!("{}: {}", key, value);
}

scores.insert(String::from("Blue"), 25);

scores.entry(String::from("Yellow")).or_insert(50);
```

The default hashing algo is called SipHash, it is fast and prevents DoS attacks.
