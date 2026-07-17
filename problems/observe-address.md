# Minimal example

## Premise

This example should demonstrate how in-place initialization lets the user get a variable's address before the variable is initialized.

This is necessary for the common use-case of making self-referential types: you need to initialize a pointer to an address inside a variable while you're in the middle of initializing it.


## Problem statement

Given the following struct `SelfRef`:

```rust
pub struct SelfRef {
    a: u32,
    addr_of_a: *const u32,
};
```

**Write a constructor `make_self_ref` that returns an instance of `SelfRef` such that `value.addr_of_a == &raw const value.a`.**


## Solution template

```rust
// FIXED DECLARATIONS

pub struct SelfRef {
    a: u32,
    addr_of_a: *const u32,
};

// PROPOSAL

fn make_self_ref(value: u32, ...) -> ...;

let value = make_self_ref(...);
assert_eq!(value.addr_of_a, &raw const value.a);
```
