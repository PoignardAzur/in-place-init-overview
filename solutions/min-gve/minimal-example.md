# Minimal example

```rust
// FIXED DECLARATIONS

pub struct MyLargeStruct { ... };


// PROPOSAL

fn create_large_struct() -> MyLargeStruct {
    MyLargeStruct {
        // ...
    }
}

// Box::new_with would be a new constructor taking a function, allocating enough space
// for its return value, and emplacing the function's return value into the allocated space.
let my_box = Box::new_with(|| create_large_struct());
```
