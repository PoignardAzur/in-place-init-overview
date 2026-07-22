# Basic composition

```rust
// FIXED DECLARATIONS

pub struct PinnedThing { ... };

pub struct Group1(PinnedThing, PinnedThing);

pub type Group2 = [PinnedThing; 3];

pub struct Group3 {
    x: PinnedThing,
}

pub enum Group4 {
    A(PinnedThing),
}

// PROPOSAL

fn new(value: u32) -> PinnedThing;

let group1: Group1 = Group1(new(1), new(2))
let group2: Group2 = [new(3), new(4), new(5)];
let group3 = Group3 {
    new(6),
};
let group4 = Group4::A(new(7));
```
