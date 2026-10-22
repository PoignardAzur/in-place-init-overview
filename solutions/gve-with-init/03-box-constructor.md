# Box constructor

```rust
// FIXED DECLARATIONS

pub struct PinnedThing { ... };


// PROPOSAL

impl !Move for PinnedThing {}

fn make_thing() -> PinnedThing;

impl<T> Box<T> {
    pub fn new_with(callback: impl FnOnce() -> T) -> Self {
        let mut allocation = Box::<T>::new_uninit();
        let ptr: *mut T = allocation.as_mut_ptr();
        unsafe {
            emplace_into!(ptr, callback());
            allocation.assume_init()
        }
    }
}

let my_box: Box<PinnedThing> = Box::new_with(|| make_thing());
```
