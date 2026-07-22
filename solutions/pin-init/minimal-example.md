# Minimal example

```rust
// FIXED DECLARATIONS

pub struct MyLargeStruct { ... };


// PROPOSAL

fn create_large_struct() -> impl Init<MyLargeStruct, E> {
    init MyLargeStruct {
        // ...
    }
}

let my_box: Box<MyLargeStruct> = Box::init(create_large_struct());
```
