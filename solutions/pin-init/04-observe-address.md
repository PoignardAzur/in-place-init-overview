# Observe address

```rust
// FIXED DECLARATIONS

pub struct SelfRef {
    a: u32,
    addr_of_a: *const u32,
}


// PROPOSAL

fn make_self_ref(value: u32) -> impl PinInit<SelfRef, Infallible> {
    pin_init!(&this in SelfRef {
        a: value,
        addr_of_a: unsafe { &raw const (*this.as_ptr()).a },
    })
}

stack_pin_init!(let value_mut: Pin<&mut SelfRef> = make_self_ref(1000));

// The pin-init proposal assumes that some kind of pin projection is accepted, so
// we can get a Pin<&mut Field> from a Pin<&mut Struct>.
assert_eq!(value_mut.addr_of_a, &raw const value_mut.a);
```
