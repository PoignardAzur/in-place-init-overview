# Fallible function

```rust
// FIXED DECLARATIONS
#[pin_data]
pub struct PinnedThing { ... }

#[pin_data]
pub struct CoupleOfThings {
    first: PinnedThing,
    second: PinnedThing,
}


// PROPOSAL

fn build() -> impl PinInit<PinnedThing, Error>;

impl CoupleOfThings {
    fn build() -> impl Init<Self, Error> {
        pin_init!(Self {
            first <- build(),
            second <- build(),
        })
    }
}
```
