# Boxed RFL Mutex

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

impl<T> !Move for Opaque<T> {}

impl<T> Opaque<T> {
    pub fn from_fn(init_func: FnOnce(*mut T)) -> Self;
}

impl<T> Mutex<T> {
    pub fn new<E>(value: T in 'self) -> Result<Self, E> {
        let mutex = Opaque::from_fn(|ptr| unsafe { bindings::__mutex_init(ptr) });
        Self { value, mutex }
    }
}

impl DriverData {
    fn new() -> Result<DriverData, Error>;
}


fn create_pinned_driver() -> Result<Pin<Box<Mutex<DriverData>>>, Error> {
    Box::pin(Mutex::new(DriverData::new()?))
}
```
