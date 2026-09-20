# Minimal example

```rust
// FIXED DECLARATIONS

pub struct MyBasicStruct {
    a: u32,
    b: u32,
    c: u32,
};


// PROPOSAL

fn create_struct(ptr: &uninit MyBasicStruct) -> &own MyBasicStruct {
    ptr <- MyLargeStruct {
        a: 0,
        b: 0,
        c: 0,
    };
    ptr
}

let my_value: MyBasicStruct <- create_struct(&uninit my_value);
```
