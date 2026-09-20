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
pub struct NamedStruct {
    x: PinnedThing,
}

pub struct TupleStruct(PinnedThing, PinnedThing);

pub type Tuple = (PinnedThing, PinnedThing);

pub type SmallArray = [PinnedThing; 3];

pub type BigArray = [PinnedThing; 1024];

pub enum Enum {
    Named { x: PinnedThing },
    Tuple(PinnedThing),
}
```

And a constructor `new` with a signature of your choice that takes an integer and returns a `PinnedThing` in-place:

```rust
fn new(value: u32, ...) -> ...;
```

**Write code that initializes an instance of each group type in-place, using values returned by `new`. Within each group, each successive call to new must take a different integer value.**


## Solution template

```rust
// FIXED DECLARATIONS

pub struct NamedStruct {
    x: PinnedThing,
}

pub struct TupleStruct(PinnedThing, PinnedThing);

pub type Tuple = (PinnedThing, PinnedThing);

pub type SmallArray = [PinnedThing; 3];

pub type BigArray = [PinnedThing; 1024];

pub enum Enum {
    Named { x: PinnedThing },
    Tuple(PinnedThing),
}


// PROPOSAL

fn new(value: u32, ...) -> ...;

let named_struct: NamedStruct = ...; // Calling (new(1))
let tuple_struct: TupleStruct = ...; // Calling (new(1), new(2))
let tuple: Tuple = ...; // Calling (new(1), new(2))
let small_array: SmallArray = ...; // Calling (new(1), new(2), new(3))
// ...
```
