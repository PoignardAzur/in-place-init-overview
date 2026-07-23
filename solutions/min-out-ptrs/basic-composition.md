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
group1 = Group1 {
    0 <- new(&uninit group1.0, 1),
    1 <- new(&uninit group1.1, 2),
};

let group2: Group2;
let [group2_0, group2_1, group2_2] = &uninit group2;
group2 <- [new(group2_0, 3), new(group2_1, 4), new(group2_2, 5)];

let group3: Group3;
group3 = Group3 {
    x <- new(&uninit group3.0, 6),
};

let group4: Group4;
let Group4::A(group4_a) = &uninit group4;
group4 = Group4::A {
    a <- new(group4_a, 7),
};
```
