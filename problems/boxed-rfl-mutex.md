# Boxed RFL Mutex

## Premise

The Rust-for-Linux project defines the following types:

```rust
#[repr(transparent)]
pub struct Opaque<T> {
    value: UnsafeCell<MaybeUninit<T>>,
    _pin: PhantomPinned,
}

pub struct Mutex<T> {
    mutex: Opaque<bindings::mutex>,
    value: UnsafeCell<T>,
}
```

(Exact declaration may differ depending on how pin-projection is implemented.)

To initialize the mutex, RFL imports a C function and type:

```rust
mod bindings {
    pub type mutex;

    pub unsafe fn __mutex_init(ptr: *mut mutex);
}
```

## Problem statement

Given an arbitrary type `DriverData` with some contents that must be pinned at initialization and remain pinned indefinitely:

```rust
pub struct DriverData { ... };
```

**Write fallible constructors for `Opaque`, `Mutex` and `DriverData`, then write a `create_pinned_driver` function with the following signature:**

```rust
fn create_pinned_driver() -> Result<Pin<Box<Mutex<DriverData>>>, Error> {
    // ...
}
```

The constructors and functions should guarantee that `Opaque::value`, `Mutex::mutex`, `Mutex::value` and `DriverData`'s contents are never moved.

(You may assume that the `Error` type is the same for all functions for simplicity.)


## Solution template

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
    // ...
}

impl<T> Mutex<T> {
    // ...
}

impl DriverData {
    // ...
}


fn create_pinned_driver() -> Result<Pin<Box<Mutex<DriverData>>>, Error> {
    // ...
}
```
