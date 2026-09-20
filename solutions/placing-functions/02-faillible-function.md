# Faillible function

```rust
// FIXED DECLARATIONS
pub struct PinnedThing { ... };

pub struct CoupleOfThings {
    first: PinnedThing,
    second: PinnedThing,
};


// PROPOSAL

#[placing]
fn build() -> Result<PinnedThing, Error>;

// **UNIMPLEMENTED: As far I know, the "Placing Functions" article doesn't explain
// how faillible emplacement would work.
// From reading the Zulip discussions, my best guess is that his preferred approach
// would be something using effect notation, e.g.
// fn build() -> PinnedThing with emplace + yeet(Error)
// See also:
// https://rust-lang.zulipchat.com/#narrow/channel/528918-t-lang.2Fin-place-init/topic/placing.20functions.20and.20interactions.20with.20effects
// https://blog.yoshuawuyts.com/a-with-based-effect-notation
```
