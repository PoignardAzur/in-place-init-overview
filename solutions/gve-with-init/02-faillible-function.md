# Faillible function

```rust
// FIXED DECLARATIONS
pub struct PinnedThing { ... };

pub struct CoupleOfThings {
    first: PinnedThing,
    second: PinnedThing,
};


// PROPOSAL

fn build() -> impl Init<PinnedThing, Error>;

impl CoupleOfThings {
    fn build() -> impl Init<Self, Error> {
        try_init! {
            let first = build()?;
            let second = build()?;
            Self { first, second }
        }
    }
}
```
