# PinInit

## Summary

This solution set tracks Alice Ryhl's [Init expressions / In-place initialization](https://hackmd.io/@aliceryhl/BJutRcPblx) article.

This article is one of the earliest proposals tracked in the in-place-init project goal. It's inspired by the [Rust-for-Linux/pin-init](https://github.com/Rust-for-Linux/pin-init/tree/dev/experimental/dyn) crate which proposes a similar syntax using macros.

As far as I'm aware, Alice no longer supports this proposal, but I've included it for completeness.

## Example preview

```rust
// MINIMAL EXAMPLE
fn create_struct() -> impl Init<MyLargeStruct, Infaillible> {
    init MyBasicStruct {
        a: 0,
        b: 0,
        c: 0,
    }
}
```
