# Observe address

```rust
// FIXED DECLARATIONS

pub struct SelfRef {
    a: u32,
    addr_of_a: *const u32,
};


// PROPOSAL

fn make_self_ref(ptr: &uninit MyLargeStruct, value: u32) -> init<'_> {
    ptr.a = value;
    ptr.addr_of_a = &raw const ptr.a;
    ptr <- _;
    ptr
}

let value: MyLargeStruct <- make_self_ref(_);
assert_eq!(value.addr_of_a, &raw const value.a);
```
