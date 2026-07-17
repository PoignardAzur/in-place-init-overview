```rust
// FIXED DECLARATIONS

mod bindings {
    pub type mutex;

    pub unsafe fn __mutex_init(ptr: *mut mutex);
}

#[repr(transparent)]
pub struct Opaque<T> {
    value: UnsafeCell<MaybeUninit<T>>,
    _pin: PhantomPinned,
}

pub struct Mutex<T> {
    mutex: Opaque<bindings::mutex>,
    value: UnsafeCell<T>,
}

pub struct DriverData { ... };

// PROPOSAL

impl<T> Opaque<T> {
    pub fn from_fn(init_func: FnOnce(*mut T)) -> impl PinInit<Self, !>;
}

impl<T> Mutex<T> {
    pub fn new_with<Err>(value: impl PinInit<T, Err>) -> impl PinInit<Self, Err> {
        create_pin_init!{
            let pin data = unwrap_pin_init!(value);
            let pin mut mutex = unwrap_pin_init!(
                Opaque::from_fn(|ptr| unsafe { bindings::__mutex_init(ptr) })
            );
            Self { value, mutex }
        }
    }
}

impl DriverData {
    fn new() -> impl PinInit<DriverData, Error>;
}


fn create_pinned_driver() -> Result<Pin<Box<Mutex<DriverData>>>, Error> {
    Box::pin_with(Mutex::new_with(DriverData::new()))
}
```
