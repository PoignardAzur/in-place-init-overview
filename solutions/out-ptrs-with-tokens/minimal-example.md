# Minimal example

```rust
// FIXED DECLARATIONS

pub struct MyBasicStruct {
    a: u32,
    b: u32,
    c: u32,
};


// PROPOSAL

fn create_struct(ptr: &uninit MyBasicStruct) -> init<'_> {
    ptr.a = 0;
    ptr.b = 0;
    ptr.c = 0;

    ptr <- _;
    ptr
}

let my_value: MyBasicStruct <- create_struct(_);
```
