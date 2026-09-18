# Minimal example

```rust
// FIXED DECLARATIONS

pub struct MyBasicStruct {
    a: u32,
    b: u32,
    c: u32,
};

// PROPOSAL

fn create_struct() -> impl Init<MyLargeStruct, Infaillible> {
    init MyBasicStruct {
        a: 0,
        b: 0,
        c: 0,
    }
}

let my_value: MyBasicStruct = init!(create_struct());
```
