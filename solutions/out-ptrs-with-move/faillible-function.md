# Faillible function

```rust
// FIXED DECLARATIONS
pub struct PinnedThing { ... };

pub struct CoupleOfThings {
    first: PinnedThing,
    second: PinnedThing,
};


// PROPOSAL

fn build(ptr: &uninit PinnedThing) -> Result<&own PinnedThing, Error>;

impl CoupleOfThings {
    fn build(ptr: &uninit CoupleOfThings) -> Result<&own CoupleOfThings, Error> {
        ptr <- TupleStruct {
            first: build(&ptr.first)?,
            second: build(&ptr.second)?,
        };
        Ok(ptr)
    }
}
```
