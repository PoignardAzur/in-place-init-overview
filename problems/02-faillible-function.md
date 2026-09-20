# Faillible function

## Premise

This is an example that demonstrates how in-place initialization handles faillible emplacement.

In non-trivial cases, a function may start writing its output into the emplacement address *before* it reaches the point where it realizes it needs to return something else.

This is necessary for any use-cases where in-place initialization might be used with I/O or locking.


## Problem statement

Given an arbitrary type `PinnedThing` and a struct `PairOfThings`:

```rust
pub struct PinnedThing { ... };

pub struct CoupleOfThings {
    first: PinnedThing,
    second: PinnedThing,
};
```

And a constructor `build()` with a signature of your choice that returns a `PinnedThing` in-place or an `Error`:

```rust
fn build(...) -> Result<..., Error>;
```

**Write a `CoupleOfThings::build()` constructor that calls `build()` twice and returns either `Self` or an `Error`.**


## Solution template

```rust
// FIXED DECLARATIONS
pub struct PinnedThing { ... };

pub struct CoupleOfThings {
    first: PinnedThing,
    second: PinnedThing,
};


// PROPOSAL

fn build(...) -> Result<..., Error>;

impl CoupleOfThings {
    // ...
}
```
