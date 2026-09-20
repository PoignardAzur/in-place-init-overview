# Out pointers with move pointers

## Summary

**Note: There isn't really a canonical "out pointers" proposal. There is a list of similar proposals, and discussions about them can be pretty fluid.**

This solution set follows the "move references" syntax that has been proposed in, among other places:

- [In-place initialization via outptrs](https://hackmd.io/awB-GOYJRlua9Cuc0a3G-Q), Jul 8 2025.
- [Thoughts on "out"-pointer](https://hackmd.io/zpPq14e3Qi6GqEc6fFcy1g?view), Nov 12 2025.

Our syntax is closer to the latter article, with no gradual initialization.


## Example previews

```rust
// MINIMAL EXAMPLE
fn create_struct(ptr: &uninit MyBasicStruct) -> &own MyBasicStruct {
    ptr <- MyLargeStruct {
        a: 0,
        b: 0,
        c: 0,
    };
    ptr
}

// BASIC COMPOSITION
let named_struct <- NamedStruct {
    x <- new(&uninit named_struct.0, 1),
};

let tuple_struct <- TupleStruct {
    0 <- new(&uninit tuple_struct.0, 1),
    1 <- new(&uninit tuple_struct.1, 2),
};
```
