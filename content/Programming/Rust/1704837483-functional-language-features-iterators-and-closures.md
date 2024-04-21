---
id: 1704837483-functional-language-features-iterators-and-closures
aliases:
  - Functional Language Features: Iterators and Closures
tags: []
---

# Functional Language Features: Iterators and Closures

Rust has a significant influence from Functional Programming, the process of using pure functions that operate without a state.

1. _Closures_: A function-like construct that you can store in a variable.
2. _Iterators_: A way of processing a series of elements.

Pattern matching and Enums are also a large part of functional programming

# Closures: Anonymous Functions that Can Capture Their Environment

Anonymous functions that can save a variable to pass as arguments to other functions, they can be created in one place and called in a different context.

## Capturing the Environment

> Every so often, our t-shirt company gives away an exclusive, limited-edition shirt to someone on our mailing list as a promotion. People on the mailing list can optionally add their favorite color to their profile. If the person chosen for a free shirt has their favorite color set, they get that color shirt. If the person hasn’t specified a favorite color, they get whatever color the company currently has the most of.

```rust
#[derive(Debug, PartialEq, Copy, Clone)]
enum ShirtColor {
  Red,
  Blue,
}

struct Inventory {
  shirts: Vec<ShirtColor>,
}

impl Inventory {
  fn giveaway(&self, user_preference: Option<ShirtColor>) -> ShirtColor {
    user_preference.unwrap_or_else(|| self.most_stocked())
  }

  fn most_stocked(&self) -> ShirtColor {
    let mut num_red = 0;
    let mut num_blue = 0;

    for color in &self.shirts {
            match color {
                ShirtColor::Red => num_red += 1,
                ShirtColor::Blue => num_blue += 1,
            }
        }
        if num_red > num_blue {
            ShirtColor::Red
        } else {
            ShirtColor::Blue
        }
  }

}

fn main() {
    let store = Inventory {
        shirts: vec![ShirtColor::Blue, ShirtColor::Red, ShirtColor::Blue],
    };

    let user_pref1 = Some(ShirtColor::Red);
    let giveaway1 = store.giveaway(user_pref1);
    println!(
        "The user with preference {:?} gets {:?}",
        user_pref1, giveaway1
    );

    let user_pref2 = None;
    let giveaway2 = store.giveaway(user_pref2);
    println!(
        "The user with preference {:?} gets {:?}",
        user_pref2, giveaway2
    );
}
```

the closure in this case is `most_stocked`, this is passed into `Option` in order to guarantee that there is a shirt color being returned.

