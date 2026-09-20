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

// **UNIMPLEMENTED: As far I know, the "Placing Functions" article doesn't explain
// how faillible emplacement would work.
```
