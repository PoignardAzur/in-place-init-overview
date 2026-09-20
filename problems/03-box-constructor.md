# Box constructor

## Premise

This example should demonstrate how a value can be initialized in a box in-place.


## Problem statement

Given an arbitrary type `PinnedThing`:

```rust
pub struct PinnedThing { ... };
```

And a constructor `make_thing()` with a signature of your choice that returns a `PinnedThing` in-place:

```rust
fn make_thing(...) -> ...;
```

**Write a constructor for `Box` that allocates space and then emplaces an object in it, and call this constructor with `make_thing()`.**

By "emplace", we mean that no instance of `PinnedThing` should move.

(Real implementations would likely include another constructor returning `Box<Pin<T>>`. We skip this for simplicity.)


## Solution template

```rust
// FIXED DECLARATIONS

pub struct PinnedThing { ... };


// PROPOSAL

fn make_thing(...) -> ...;

impl<T> Box<T> {
    // ...
    // Something like `fn emplace(...) -> Self`
    // ...
}

let my_box: Box<PinnedThing>;
// ...
// initialize my_box somehow, without ever moving PinnedThing.
// ...
```
