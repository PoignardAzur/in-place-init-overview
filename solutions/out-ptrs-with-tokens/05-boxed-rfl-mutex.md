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
    pub unsafe fn ffi_init(
        &uninit self,
        init_fn: FnOnce(*mut T),
    ) -> init<'_> {
        self <- Self {
            value: UnsafeCell::new(MaybeUninit::uninit()),
            _pin: PhantomPinned,
        };
        init_fn(self.value.get() as *mut T);
        self
    }
}

impl<T> Mutex<T> {
    pub fn new<E>(
        &uninit self,
        init_fn: impl for<'a> FnOnce(&'a uninit T) -> Result<init<'a>, E>,
    ) -> Result<init<'_>, E> {
        self.mutex <- unsafe {
            Opaque::ffi_init(_, |ptr| unsafe { bindings::__mutex_init(ptr); })
        };
        self.value <- init_fn(_)?;
        self <- _;
        Ok(self)
    }
}

impl DriverData {
    pub fn new(
        &uninit self,
    ) -> Result<init<'_>, Error>;
}

impl Box<T> {
    pub fn try_pin_with<E>(
        &uninit self,
        init_fn: impl for<'a> FnOnce(&'a uninit T) -> Result<init<'a>, E>,
    ) -> Result<Pin<Box<T>>, E>;
}


fn create_pinned_driver() -> Result<Pin<Box<Mutex<DriverData>>>, Error> {
    Box::try_pin_with(
        |ptr| Mutex::new_with(ptr, |ptr| DriverData::new(ptr))
    )
}
```
