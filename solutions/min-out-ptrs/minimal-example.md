# Minimal example

```rust
// FIXED DECLARATIONS

pub struct MyLargeStruct { ... };


// PROPOSAL

fn create_large_struct(a: &uninit MyLargeStruct) -> &own MyLargeStruct {
    a <- MyLargeStruct {
        // ...
    }
}

// pub fn Box::new_init(
//   ctor: impl for<'a> FnOnce(&'a uninit T) -> &'a own T,
// ) -> Self;
let my_box = Box::new_init(create_large_struct);
