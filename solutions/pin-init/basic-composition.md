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

fn new(value: u32) -> impl Init<PinnedThing, Infaillible>

let named_struct: impl Init<NamedStruct> = init NamedStruct { x: new(1) };
let tuple_struct: impl Init<TupleStruct> = init TupleStruct(new(1), new(2));
let tuple: impl Init<Tuple> = init (new(1), new(2));
let small_array: impl Init<SmallArray> = init [new(1), new(2), new(3)];
let big_array: impl Init<BigArray> = todo!("See below");
let enum_named: impl Init<Enum> = init Enum::Named { x: new(1) };
let enum_tuple: impl Init<Enum> = init Enum::Tuple(new(1)),

// Array repetition with same value:
let big_array: impl Init<BigArray> = init [new(1), 1024];

// Array repetition with changing value:
let big_array: impl Init<BigArray> = init_from_fn(|i| new(i)).into_ok();

// init_from_fn would likely be provided by the standard library with this signature:
fn init_from_fn<T, E, const N: usize>(f: impl FnMut(usize) -> impl Init<T, E>)
    -> impl Init<[T; N], E>;
```
