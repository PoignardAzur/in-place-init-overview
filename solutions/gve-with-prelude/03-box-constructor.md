# Box constructor

```rust
// FIXED DECLARATIONS

pub struct PinnedThing { ... };


// PROPOSAL

fn make_thing() -> PinnedThing;

impl<T> Box<T> {
    // `in 'self` means that the input ptr is derived from something computed
    // before the function arguments are evaluated.
    fn new(_value: T in 'self) -> Box<T> {
        // Values defined here are preserved from prelude to main function body.
        let alloc;
        prelude {
            alloc = Box::new_uninit();
            // prelude returns a tuple of input pointers, one for each argument
            // using `in 'self`.
            (alloc.as_ptr(),)
        }
        unsafe { alloc.assume_init() }
     }
}

let my_box: Box<PinnedThing> = Box::new(make_thing());
```
