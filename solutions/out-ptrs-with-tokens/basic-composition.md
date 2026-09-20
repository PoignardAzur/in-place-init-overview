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

fn new(ptr: &uninit PinnedThing, value: u32) -> &own PinnedThing;

let named_struct: NamedStruct;
named_struct.x <- new(&uninit named_struct.x, 1);
named_struct <- _;

let tuple_struct: TupleStruct;
tuple_struct.0 <- new(&uninit tuple_struct.0, 1);
tuple_struct.1 <- new(&uninit tuple_struct.1, 2);
tuple_struct <- _;

let tuple: Tuple;
tuple.0 <- new(&uninit tuple.0, 1);
tuple.1 <- new(&uninit tuple.1, 2);
tuple <- _;

let small_array: SmallArray;
small_array[0] <- new(&uninit small_array[0], 1);
small_array[1] <- new(&uninit small_array[1], 2);
small_array[2] <- new(&uninit small_array[2], 3);
small_array <- _;

// This function would likely be provided by the standard library
fn init_from_fn<T, const N: usize>(array: &uninit [T; N], f: impl FnMut(usize) -> T)
    -> &own [T; N];
let big_array: BigArray;
big_array = init_from_fn(&uninit big_array, |i| new(i));

// **UNIMPLEMENTED: As far I know, no "out pointers" proposals suggests how to initialize an enum.**
let enum_tuple: Enum;
```
