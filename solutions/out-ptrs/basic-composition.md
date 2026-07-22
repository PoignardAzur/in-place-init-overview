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

fn new(&uninit PinnedThing, value: u32) -> &own PinnedThing;

let group1: Group1;
group1.0 <- new(&uninit group1.0, 1);
group1.1 <- new(&uninit group1.1, 2);
group1 <- _;

let group2: Group2;
group2[0] <- new(&uninit group2[0], 1);
group2[1] <- new(&uninit group2[1], 2);
group2[2] <- new(&uninit group2[2], 2);
group2 <- _;

let group3: Group3;
group3.x <- new(&uninit group3.x, 1);
group3 <- _;

// **UNIMPLEMENTED: As far I know, no "out pointers" proposals suggests how to initialize an enum.**
let group4: Group4;
```
