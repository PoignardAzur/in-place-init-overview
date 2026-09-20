# Basic composition

```rust
// FIXED DECLARATIONS

pub struct NamedStruct {
    x: PinnedThing,
}

pub struct TupleStruct(PinnedThing, PinnedThing);

pub type Tuple = (PinnedThing, PinnedThing);

pub type SmallArray = [PinnedThing; 3];

pub type BigArray = [PinnedThing; 1024];

pub enum Enum {
    Named { x: PinnedThing },
    Tuple(PinnedThing),
}


// PROPOSAL

fn new(value: u32) -> PinnedThing;

let named_struct: NamedStruct = NamedStruct { x: new(1) };
let tuple_struct: TupleStruct = TupleStruct { 0: new(1), 1: new(2) };
let tuple: Tuple = (new(1), new(2));
let small_array: SmallArray = [new(1), new(2), new(3)];
let big_array: BigArray = core::array::from_fn(|i| new(i));
let enum_named: Enum = Enum::Named { x: new(1) };
let enum_tuple: Enum = Enum::Tuple { 0: new(1) };
```
