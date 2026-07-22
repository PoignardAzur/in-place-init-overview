# Observe address

```rust
// FIXED DECLARATIONS

pub struct SelfRef {
    a: u32,
    addr_of_a: *const u32,
};

// PROPOSAL

fn make_self_ref(value: u32) -> impl PinInit<SelfRef, Infaillible> {
    pin_init!(SelfRef {
        a: value,
        addr_of_a: &raw const a,
    })
}

let value_mut: Pin<&mut SelfRef> = pinit!(make_self_ref(1000));

// The pin-init proposal assumes that some kind of pin projection is accepted, so
// we can get a Pin<&mut Field> from a Pin<&mut Struct>.
assert_eq!(value_mut.addr_of_a, &raw const value_mut.a);
```
