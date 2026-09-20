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

impl<T> Opaque<T> {
    pub unsafe fn ffi_init(init_func: FnOnce(*mut T)) -> impl PinInit<Self> {
        init Self {
            value: UnsafeCell::new(MaybeUninit::uninit()),
            _pin: PhantomPinned,
            _: {
                init_fn(value.get() as *mut T);
            }
        };
    }
}

impl<T> Mutex<T> {
    pub fn new<E>(
        value: impl PinInit<T, E>,
    ) -> impl PinInit<Self, E> {
        init Self {
            mutex <- Opaque::ffi_init(|ptr| unsafe { bindings::__mutex_init(ptr) }),
            value <- UnsafeCell::pin_init(value),
        }
    }
}

impl DriverData {
    fn new() -> impl PinInit<DriverData, Error>;
}

impl Box<T> {
    pub fn pin_init<E>(value: impl PinInit<T, E>) -> Result<Pin<Box<T>>, E>;
}


fn create_pinned_driver() -> Result<Pin<Box<Mutex<DriverData>>>, Error> {
    Box::pin_init(Mutex::new(DriverData::new()))
}
```
