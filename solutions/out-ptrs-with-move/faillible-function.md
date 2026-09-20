# Faillible function

```rust
// FIXED DECLARATIONS
pub struct PinnedThing { ... };

pub struct CoupleOfThings {
    first: PinnedThing,
    second: PinnedThing,
};

// PROPOSAL
fn build(ptr: &uninit PinnedThing) -> Result<&out PinnedThing, Error>;

impl CoupleOfThings {
    fn build(ptr: &uninit CoupleOfThings) -> Result<&out CoupleOfThings, Error> {
        ptr <- TupleStruct {
            first: build(&ptr.first)?,
            second: build(&ptr.second)?,
        };
        Ok(ptr)
    }
}
```
