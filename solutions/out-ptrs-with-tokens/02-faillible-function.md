# Faillible function

```rust
// FIXED DECLARATIONS
pub struct PinnedThing { ... };

pub struct CoupleOfThings {
    first: PinnedThing,
    second: PinnedThing,
};


// PROPOSAL

fn build(ptr: &uninit PinnedThing) -> Result<init<'_>, Error>;

impl CoupleOfThings {
    fn build(ptr: &uninit CoupleOfThings) -> Result<init<'_>, Error> {
        ptr.first <- build(_)?;
        ptr.second <- build(_)?;
        ptr <- _;
        Ok(ptr)
    }
}
```
