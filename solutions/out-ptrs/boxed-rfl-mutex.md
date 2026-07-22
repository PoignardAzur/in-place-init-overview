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
    pub fn try_ffi_init<E>(
        &uninit self,
        init_fn: FnOnce(*mut T) -> Result<(), E>
    ) -> Result<&own Self, E> {
        init_fn(self as *mut self)?;
        Ok(assume_init(self))
    }
}

impl<T> Mutex<T> {
    pub fn new(
        &uninit self,
        init_fn: impl for<'a> FnOnce(&'a uninit T) -> Result<&'a own T, Error>,
    ) -> Result<&own Self, Error>
    {
        self.mutex <- Opaque::try_ffi_init::<Infaillible>(
            &uninit self.mutex,
            |ptr| unsafe {
                bindings::__mutex_init(ptr);
                Ok(())
            }
        );
        self.value <- init_fn(&uninit self.value)?;
        self <- _;
        Ok(self)
    }
}

impl DriverData {
    pub fn new(
        &uninit self,
    ) -> Result<&own Self, Error>;
}


fn create_pinned_driver() -> Result<Pin<Box<Mutex<DriverData>>>, Error> {
    Box::pin_with(
        |ptr| Mutex::new_with(ptr, |ptr| DriverData::new(ptr))
    )
}
```
