# Guaranteed Value Emplacement With Function Preludes

## Summary

This solution set tracks Alice Ryhl's [Guaranteed value emplacement](https://hackmd.io/@aliceryhl/BJ4rjbYaZl) article.

That article is similar to the initial ["Guaranteed Value Emplacement" RFC draft](https://hackmd.io/@s_haMSbyTAOWfoXc1aYNUg/ByfXTuHqxg), with some additions:

- Functions can have multiple "out pointers" they can emplace values into, including out pointers for enum variants.
- Functions may have "preludes" which run before their arguments are evaluated. These preludes are how `Box::new()` can use emplacement by default without breaking changes.

See the linked article for more details.


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
- [#t-lang/in-place-init > &#91;blog&#93; Placing Functions](https://rust-lang.zulipchat.com/#narrow/channel/528918-t-lang.2Fin-place-init/topic/.5Bblog.5D.20Placing.20Functions/with/527735465)
