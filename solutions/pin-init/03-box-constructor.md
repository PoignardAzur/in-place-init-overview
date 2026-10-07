# Box constructor


```rust
// FIXED DECLARATIONS

pub struct PinnedThing { ... }


// PROPOSAL

fn make_thing() -> impl PinInit<PinnedThing, Infallible>;

impl<T> Box<T> {
    pub fn init(i: impl PinInit<T, Infallible>) -> Box<T> {
        let allocation = Box::<T>::new_uninit();

        unsafe {
            let () = i.init(allocation.as_mut_ptr()).into_ok();
            allocation.assume_init()
        }
    }
}

let my_box: Box<PinnedThing> = Box::init(make_thing());
```
