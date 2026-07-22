# Observe address

```rust
// FIXED DECLARATIONS

pub struct SelfRef {
    a: u32,
    addr_of_a: *const u32,
};

// PROPOSAL

fn make_self_ref(ptr: &uninit MyLargeStruct, value: u32) -> &own MyLargeStruct {
    ptr.a = value;
    ptr.addr_of_a = &raw const ptr.a;
    ptr <- _;
    ptr
}

let value: MyLargeStruct;
value = *make_self_ref(&uninit value);
assert_eq!(value.addr_of_a, &raw const value.a);
```
