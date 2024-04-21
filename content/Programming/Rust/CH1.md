---
id: CH1
aliases:
  - CH1
tags: []
---

# CH1

## Hello, World!

```rust
fn main() {
    println!("Hello, world!");
}
```

### Anatomy of a Rust Program

To define a function, the `fn` keyword is used, and just like C, `main` is a special function keyword that denotes where the program should start

The `println!()` function is used to push a string to the console. the ! is because this is a macro, and all lines are ended with semicolons

## Cargo

Cargo is rust's package manager and build system, it can be used to manage projects

the most used commands are:

```bash
cargo new project_name # create new cargo project
cargo build # Build Cargo project
cargo build --release # Build for release
cargo run # Run Cargo Project
cargo check # Checks code for compilation errors
```
