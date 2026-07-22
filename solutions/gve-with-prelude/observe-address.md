# Observe address

```rust
// FIXED DECLARATIONS

pub struct SelfRef {
    a: u32,
    addr_of_a: *const u32,
};
// PROPOSAL

fn make_self_ref(value: u32) -> SelfRef {
    let mut ret = SelfRef {
        a: value,
        addr_of_a: std::ptr::null();
    };
    ret.addr_of_a = &raw const ret.a;
    ret
}

let value = make_self_ref();
assert_eq!(value.addr_of_a, &raw const value.a);
```
