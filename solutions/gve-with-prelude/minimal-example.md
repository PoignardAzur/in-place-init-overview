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

let my_box: Box<MyLargeStruct> = Box::new(create_large_struct());
```
