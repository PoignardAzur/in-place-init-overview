# Box constructor


```rust
// FIXED DECLARATIONS

pub struct PinnedThing { ... };


// PROPOSAL

fn make_thing(ptr: &uninit PinnedThing) -> &own PinnedThing;

impl<T> Box<T> {
    fn new_with(callback: impl for<'a> FnOnce(&'a uninit T) -> &'a own T) -> Self {
        let allocation = Box::<T>::new_uninit();
        let ptr: &uninit T = &uninit *allocation;

        let init = callback(ptr);

        // We disarm the &own T and immediately return Box<T>
        std::mem::forget(init);
        unsafe { allocation.assume_init() }
    }
}

let my_box: Box<PinnedThing> = Box::new_with(make_thing);
