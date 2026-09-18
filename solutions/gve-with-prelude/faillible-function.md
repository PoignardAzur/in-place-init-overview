# Faillible function

```rust
// FIXED DECLARATIONS
pub struct PinnedThing { ... };

pub struct CoupleOfThings {
    first: PinnedThing,
    second: PinnedThing,
};

// PROPOSAL
fn build() -> Result<PinnedThing, Error>;

impl CoupleOfThings {
    fn build() -> Result<Self, Error> {
        let first = build()?;
        let second = build()?;
        Self { first, second }
    }
}
```
