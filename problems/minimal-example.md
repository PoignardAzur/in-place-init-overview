# Minimal example

## Premise

This example should demonstrate the minimum viable syntax for returning a large object from a function without moving it.


## Problem statement

Given a type `MyBasicStruct`:

```rust
pub struct MyBasicStruct {
    a: u32,
    b: u32,
    c: u32,
};
```

**Write a function returning `MyBasicStruct` (setting fields to zero), and then call this function in a way that emplaces its result in a local.**

By "emplace", we mean that no instance of `MyBasicStruct` is ever moved.
What this means specifically will be explored in other examples.


## Solution template

```rust
// FIXED DECLARATIONS

pub struct MyBasicStruct {
    a: u32,
    b: u32,
    c: u32,
};


// PROPOSAL

fn create_struct(...) -> ... {
    // ...
}

let my_value: MyBasicStruct;
// ...
// initialize my_value somehow, without ever moving MyBasicStruct.
// ...
```
