# Basic composition

## Premise

This is a series of short examples to demonstrate how in-place-initialization can be composed.

By "composed", we mean "you can initialize large types in-place by initializing small types in-place".


## Problem statement

Given an arbitrary type `PinnedThing`:

```rust
pub struct PinnedThing { ... };
```

A list of composite types:

```rust
pub struct Group1(PinnedThing, PinnedThing);

pub type Group2 = [PinnedThing; 3];

pub struct Group3 {
    x: PinnedThing,
}

pub enum Group4 {
    A(PinnedThing),
}
```

And a constructor `new` with a signature of your choice that takes an integer and returns a `PinnedThing` in-place:

```rust
fn new(value: u32, ...) -> ...;
```

**Write code that initializes an instance of each group type in-place, using values returned by `new`. Each successive call to new must take a different integer value.**


## Solution template

```rust
// FIXED DECLARATIONS

pub struct PinnedThing { ... };

pub struct Group1(PinnedThing, PinnedThing);

pub type Group2 = [PinnedThing; 3];

pub struct Group3 {
    x: PinnedThing,
}

pub enum Group4 {
    A(PinnedThing),
}

// PROPOSAL

fn new(value: u32, ...) -> ...;

let group1: Group1 = ...; // Calling (new(1), new(2))
let group2: Group2 = ...; // Calling (new(3), new(4), new(5))
// ...
```
