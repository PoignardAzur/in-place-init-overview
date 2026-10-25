# Basic composition

```rust
// FIXED DECLARATIONS

#[pin_data]
pub struct NamedStruct {
    #[pin]
    x: PinnedThing,
}

#[pin_data]
pub struct TupleStruct(#[pin] PinnedThing, #[pin] PinnedThing);

pub type Tuple = (PinnedThing, PinnedThing);

pub type SmallArray = [PinnedThing; 3];

pub type BigArray = [PinnedThing; 1024];

pub enum Enum {
    Named { x: PinnedThing },
    Tuple(PinnedThing),
}


// PROPOSAL

fn new(value: u32) -> impl PinInit<PinnedThing, Infallible>;

let named_struct: impl PinInit<NamedStruct> = pin_init!(NamedStruct { x <- new(1) });
// TODO(benno): verify this syntax
let tuple_struct: impl PinInit<TupleStruct> = pin_init!(TupleStruct(<- new(1), <- new(2)));

let small_array: impl PinInit<SmallArray> = init init_array_fn(|i| new(i + 1));
// Array repetition with same value:
let big_array: impl PinInit<BigArray> = init_array_fn(|i| new(1));
// Array repetition with changing value:
let big_array: impl PinInit<BigArray> = init_from_fn(|i| new(i)).into_ok();

fn init_from_fn<T, E, const N: usize>(f: impl FnMut(usize) -> impl PinInit<T, E>)
    -> impl PinInit<[T; N], E>;

let enum_named: impl PinInit<Enum> = /* UNSUPPORTED */;
let enum_tuple: impl PinInit<Enum> = /* UNSUPPORTED */;
let tuple: impl PinInit<Tuple> = /* UNSUPPORTED */;
```
