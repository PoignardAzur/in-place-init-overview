# in-place-init-overview

This repository is an overview of proposals for adding [in-place initialization](https://github.com/rust-lang/goals/issues/395) to the Rust programming language.

This repository has two parts:

- A list of problems representing things that an in-place-init feature will be expected to do.
- For each major in-place-init proposal, a list of code examples showing how that proposal would address each given problem.

(This is based on similar previous efforts like @BennoLossin's [in-place-init-proposals](https://github.com/BennoLossin/in-place-init-proposals))

While I've tried to keep the problems and solutions pretty standardized and to stick to each proposal's published syntax as much as possible, some of the solutions may be a little speculative and pseudo-code-ish.

Feel free to make a PR if you think a given proposal would (as stated in its published version) solve a problem differently.


## Problems

- [minimal-example](problems/00-minimal-example.md)
- [basic-composition](problems/01-basic-composition.md)
- [faillible-function](problems/02-faillible-function.md)
- [box-constructor](problems/03-box-constructor.md)
- [observe-address](problems/04-observe-address.md)
- [boxed-rfl-mutex](problems/05-boxed-rfl-mutex.md)
- [asahi-monster-struct](problems/06-asahi-monster-struct.md)

## Proposals

- [gve-with-init](solutions/gve-with-init)
- [gve-with-prelude](solutions/gve-with-prelude)
- [out-ptrs-with-move](solutions/out-ptrs-with-move)
- [out-ptrs-with-tokens](solutions/out-ptrs-with-tokens)
- [pin-init](solutions/pin-init)

## See also

- https://github.com/rust-lang/beyond-refs/blob/main/src/in-place-init.md#potential-design-axioms
- https://rust-lang.zulipchat.com/#narrow/channel/528918-t-lang.2Fin-place-init/topic/in-place.20initialization.3A.20RfL.20design.20wishes/with/539083811
