# Box constructor


```rust
// FIXED DECLARATIONS

pub struct PinnedThing { ... };


// PROPOSAL

fn make_thing() -> impl Init<PinnedThing, Infaillible>;

impl<T> Box<T> {
    pub fn init(i: impl Init<T, Infallible>) -> Box<T> {
        let allocation = Box::<T>::new_uninit();

        let () = i.init(allocation.as_mut_ptr()).into_ok();
        unsafe { allocation.assume_init() }
    }
}

let my_box: Box<PinnedThing> = Box::init(make_thing());
```
