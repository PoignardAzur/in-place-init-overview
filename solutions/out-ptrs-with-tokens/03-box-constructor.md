# Box constructor


```rust
// FIXED DECLARATIONS

pub struct PinnedThing { ... };


// PROPOSAL

fn make_thing(ptr: &uninit PinnedThing) -> init<'_>;

impl<T> Box<T> {
    fn new_with(callback: impl for<'a> FnOnce(&'a uninit T) -> init<'a>) -> Self {
        let allocation = Box::<T>::new_uninit();
        let ptr: &uninit T = &uninit *allocation;

        let init = callback(ptr);

        // We disarm the init<'_> and immediately return Box<T>
        unsafe {
            init.discharge();
            allocation.assume_init() 
        }
    }
}

let my_box: Box<PinnedThing> = Box::new_with(make_thing);
