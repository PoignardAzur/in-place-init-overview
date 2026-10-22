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
    pub unsafe fn from_fn(init_func: FnOnce(*mut T)) -> Self {
        let opaque = Self {
            value: UnsafeCell::new(MaybeUninit::uninit()),
            _pin: PhantomPinned,
        };
        init_fn(opaque.value.get() as *mut T);
        opaque
    }
}

impl<T> Mutex<T> {
    pub fn new_init<E>(value: impl PinInit<T, E>) -> impl PinInit<Self, E> {
        pin_init!{
            let data = value?;
            let mutex = unsafe {
                Opaque::from_fn(|ptr| unsafe { bindings::__mutex_init(ptr) })
            };
            Self { value, mutex }
        }
    }
}

impl DriverData {
    fn new() -> impl Init<DriverData, Error>;
}

impl Box<T> {
    pub fn new_init<E>(value: impl Init<T, E>) -> Result<Box<T>, E>;
}


fn create_pinned_driver() -> Result<Box<Mutex<DriverData>>, Error> {
    let mutex = Mutex::new_init(DriverData::new());
    let boxed_mutex = Box::new_init(new)?;
    Ok(Box::into_pin(boxed_mutex))
}
```
