# Guaranteed Value Emplacement with Init trait

## Summary

This is based on the [Minimal Guaranteed Value Emplacement (min-GVE)](https://hackmd.io/@s_haMSbyTAOWfoXc1aYNUg/rylb1KLoMx) proposal.

## Example previews

```rust
// MINIMAL EXAMPLE
fn create_struct() -> MyBasicStruct {
    MyBasicStruct {
        a: 0,
        b: 0,
        c: 0,
    }
}

// OBSERVE ADDRESS
fn make_self_ref(value: u32) -> SelfRef {
    let mut ret = SelfRef {
        a: value,
        addr_of_a: std::ptr::null();
    };
    ret.addr_of_a = &raw const ret.a;
    ret
}
```


## More info

- [#t-lang/in-place-init > RFC Draft: Guaranteed Value Emplacement](https://rust-lang.zulipchat.com/#narrow/channel/528918-t-lang.2Fin-place-init/topic/RFC.20Draft.3A.20Guaranteed.20Value.20Emplacement/with/545850965)
