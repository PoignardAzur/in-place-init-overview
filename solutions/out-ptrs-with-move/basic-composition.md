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
NamedStruct = NamedStruct {
    x <- new(&uninit named_struct.0, 1),
};

let tuple_struct: TupleStruct;
TupleStruct = TupleStruct {
    0 <- new(&uninit tuple_struct.0, 1),
    1 <- new(&uninit tuple_struct.1, 2),
};

let tuple: Tuple;
Tuple = (new(&uninit tuple.0, 1), new(&uninit tuple.1, 2));

let small_array: SmallArray;
let [SmallArray_0, SmallArray_1, SmallArray_2] = &uninit small_array;
SmallArray <- [new(SmallArray_0, 1), new(SmallArray_1, 2), new(SmallArray_2, 3)];

// This function would likely be provided by the standard library
fn init_from_fn<T, const N: usize>(array: &uninit [T; N], f: impl FnMut(usize) -> T)
    -> &own [T; N];
let big_array: BigArray;
big_array = init_from_fn(&uninit big_array, |i| new(i));

let enum_named: Enum;
let Enum::Named { x: enum_named } = &uninit enum_named;
enum_named = Enum::Tuple {
    a <- new(enum_named, 1),
};

let enum_tuple: Enum;
let Enum::Tuple(enum_tuple) = &uninit enum_tuple;
enum_tuple = Enum::Tuple {
    a <- new(enum_tuple, 1),
};
```
