# `pin-init` crate

## Summary

This solution set tracks Gary Guo's and Benno Lossin's crate [`pin-init`](https://github.com/Rust-for-Linux/pin-init) that is used in the Linux kernel for in-place initialization.

## Example preview

```rust
// MINIMAL EXAMPLE
fn create_struct() -> impl PinInit<MyLargeStruct, Infallible> {
    pin_init!(MyBasicStruct {
        a: 0,
        b: 0,
        c: 0,
    })
}
```
