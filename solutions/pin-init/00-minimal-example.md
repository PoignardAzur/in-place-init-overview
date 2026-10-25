# Minimal example

```rust
// FIXED DECLARATIONS

pub struct MyBasicStruct {
    a: u32,
    b: u32,
    c: u32,
}


// PROPOSAL

fn create_struct() -> impl Init<MyLargeStruct, Infallible> {
    pin_init!(MyBasicStruct {
        a: 0,
        b: 0,
        c: 0,
    })
}

stack_pin_init!(let my_value: MyBasicStruct = create_struct());
```
