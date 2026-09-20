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

fn new(ptr: &uninit PinnedThing, value: u32) -> init<'_>;

let named_struct: NamedStruct;
named_struct.x <- new(_, 1);
named_struct <- _;

let tuple_struct: TupleStruct;
tuple_struct.0 <- new(_, 1);
tuple_struct.1 <- new(_, 2);
tuple_struct <- _;

let tuple: Tuple;
tuple.0 <- new(_, 1);
tuple.1 <- new(_, 2);
tuple <- _;

let small_array: SmallArray;
small_array[0] <- new(_, 1);
small_array[1] <- new(_, 2);
small_array[2] <- new(_, 3);
small_array <- _;

// This function would likely be provided by the standard library
fn init_from_fn<T, const N: usize>(array: &uninit [T; N], f: impl FnMut(usize) -> T)
    -> &own [T; N];
let big_array: BigArray <- init_from_fn(_, |i| new(i));

// **UNIMPLEMENTED: As far I know, no "out pointers" proposals suggests how to initialize an enum.**
// There is no mention of enums in https://github.com/rust-lang/beyond-refs/blob/5e2b3de108a96c93adc594acd3165aaf5b78c81b/src/in-place-init/uninit-ref.md
let enum_tuple: Enum;
```
