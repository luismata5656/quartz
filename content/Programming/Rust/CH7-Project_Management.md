---
id: CH7
aliases: []
tags: []
---

# Project_Management

Cargo has many features that promotes clean code and project management

1. Packages - A Cargo feature that lets you build, test, and share crates
2. Crates - A tree of modules that produces a library or executable
3. Modules and use - Let you control the organization, scope, and privacy of paths
4. Paths - A way of naming an item, such as a struct, function, or module

# Packages and Crates

A _crate_ is the smallest unit of code that Rust considers at a time. crates can contain modules that are defined in other files to later get compiled with the crate.

A crate can be a binary or a library, the difference is that a binary crate can be executed and has a `main` function, while library crates define functionality intended to be shared with multiple projects.

A package containes one or more crates and provides a set of functionality. A package contains a `Cargo.toml` file that describes how to build those crates.

To create a package, run `cargo new <package_name>`

# Defining Modules to control Scope and Privacy

1. When compiling a crate, the compiler first looks in the crate root file, `lib.rx` for a library, and `main.rs` for a binary.
2. in this file, you can declare new modules with the `mod` keyword. The compiler will then search for the code for that module:

- Inline, withing the current file
- in the `module.rs`
- in the `module` directory in a file named `mod.rs`

3. In any other file than the crate root, submodules can be made in the same way modules are made in the crate root. These are searched for in:

- Inline, within the current file
- in the `module/submodule.rs`
- in the `module/submodule/mod.rs`

4. Once a module is part of the crate, code within that crate can refer to that module anywhere as long as privacy rules allow.
5. Code within a module is private from the parent modules, to make a module public, it can be declared with `pub mod module_name`
6. within a scope, `use` will create shortcuts to modules, functions, and other items. `use` can be used to bring a module into scope, it can also be used to bring a function into scope with `use crate::module::function` or `use crate::module::function as alias`

Here is an example:

```
backyard
├── Cargo.lock
├── Cargo.toml
└── src
    ├── garden
    │   └── vegetables.rs
    ├── garden.rs
    └── main.rs
```

_main.rs_

```rust
use crate::garden::vegetables::Asparagus;

pub mod garden;

fn main() {
    let plant = Asparagus {};
    println!("I'm growing {:?}!", plant);
}
```

_garden.rs_

```rust
pub mod vegetables;
```

`vegetables` has a `mod.rs` file that defines the `Asparagus` struct
`vegetables.rs`

```rust
pub struct Asparagus {}
```

# Paths for Referring to an Item in the Module Tree

To refer to an item in a module, you can use a path. A path can take two forms:

- Absolute: the full path from the crate root. Starts with a crate name or a literal `crate`
- relative: starts from the current module and uses `self`, `super`, or an identifier in the current module

# Bringing Paths into Scope with the `use` keyword

when you `use` a module, you bring it into scope, so you can refer to it without the full path.

```rust

mod front_of_house {
    pub mod hosting {
        pub fn add_to_waitlist() {}
    }
}

use crate::front_of_house::hosting;

pub fn eat_at_restaurant() {
    hosting::add_to_waitlist();
}
```

this is like creating a symbolic link, though this is only in the current scope, so children do not get access to it.

```rust
mod customer {
    pub fn eat_at_restaurant() {
        super::front_of_house::hosting::add_to_waitlist(); // ERROR
    }
}
```

## Creating Idiomatic `use` Paths

when bringing moduless into scope, it is also possible to simply bring in whatever function you need from that module:

```rust
use std::collections::HashMap;
```

This works and is encouraged in the community, but it can also be done like this:

```rust
use std::collections;
```

The second example can prevent from possibly making something or using something also called HashMap and thus creating confusion for the compiler.

## Providing New Names with the `as` Keyword

the `as` keyword can also be used to prevent bringing in two types of the same name:

```rust
use std::fmt::Result;
use std::io::Result as IoResult;
```

## Re-exporting Names with `pub use`

`pub use` can be used to bring in a module and re-export it as public:

```rust
mod front_of_house {
    pub mod hosting {
        pub fn add_to_waitlist() {}
    }
}

pub use crate::front_of_house::hosting;

pub fn eat_at_restaurant() {
    hosting::add_to_waitlist();
}
```

## Using Nested paths to clean up Large `use` Lists

```rust
// --snip--
use std::cmp::Ordering;
use std::io;
// --snip--
```

Nested paths let you do this:

```rust
use std::{cmp::Ordering, io};
```

## Using the `glob` Operator to Bring All Public Items into Scope

```rust
use std::collections::*;
```

This brings all public items into scope, but is not recommended for use in production code.
