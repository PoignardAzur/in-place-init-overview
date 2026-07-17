# Minimal example

## Premise

This example should demonstrate the minimum viable syntax for returning a large object from a function without moving it.


## Problem statement

Given an arbitrary type `MyLargeStruct`:

```rust
pub struct MyLargeStruct { ... };
```

**Write a function returning `MyLargeStruct`, and then call this function in a way that emplaces its result in a box.**

By "emplace", we mean that no instance of `MyLargeStruct` is ever moved.
What this means specifically will be explored in other examples.


## Solution template

```rust
// FIXED DECLARATIONS

pub struct MyLargeStruct { ... };


// PROPOSAL

fn create_large_struct(...) -> ... {
    // ...
}

let my_box: Box<MyLargeStruct>;
// ...
// initialize my_box somehow, without ever moving MyLargeStruct.
// ...
```
