# Guaranteed Value Emplacement with Init trait

## Summary

This solution set tracks [Yosh Wuyts'](https://blog.yoshuawuyts.com/placing-functions/) article.

Yosh has suggested he might write a more formal proposal eventually. In the meantime, this solution set might not reflect his exact vision for placing functions.

Consider this a best guess at what the proposal would look like.


## Example previews

```rust
#[placing]
fn make_self_ref(value: u32) -> SelfRef {
    super let mut ret = SelfRef {
        a: value,
        addr_of_a: std::ptr::null();
    };
    ret.addr_of_a = &raw const ret.a;
    ret
}
```

## More info

- [#t-lang/in-place-init > &#91;blog&#93; Placing Functions](https://rust-lang.zulipchat.com/#narrow/channel/528918-t-lang.2Fin-place-init/topic/.5Bblog.5D.20Placing.20Functions/with/527735465)
- [#t-lang/in-place-init > &#91;blog&#93; Four levels of in-place initialization](https://rust-lang.zulipchat.com/#narrow/channel/528918-t-lang.2Fin-place-init/topic/.5Bblog.5D.20Four.20levels.20of.20in-place.20initialization/with/616697846)
