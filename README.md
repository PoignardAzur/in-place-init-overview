# in-place-init-overview

This repository is an overview of proposals for adding [in-place initialization](https://github.com/rust-lang/goals/issues/395) to the Rust programming language.

This repository has two parts:

- A list of problems representing things that an in-place-init feature will be expected to do.
- For each major in-place-init proposal, a list of code examples showing how that proposal would address each given problem.

(This is based on similar previous efforts like @BennoLossin's [in-place-init-proposals](https://github.com/BennoLossin/in-place-init-proposals))

While I've tried to keep the problems and solutions pretty standardized and to stick to each proposal's published syntax as much as possible, some of the solutions may be a little speculative and pseudo-code-ish.

Feel free to make a PR if you think a given proposal would (as stated in its published version) solve a problem differently.


## Proposals

- [gve-with-init](solutions/gve-with-init)
- [gve-with-prelude](solutions/gve-with-prelude)
- [out-ptrs-with-move](solutions/out-ptrs-with-move)
- [out-ptrs-with-tokens](solutions/out-ptrs-with-tokens)
- [pin-init](solutions/pin-init)

## Problems

You should consult problems in this order:

- **minimal-example**
- **basic-composition**
- **faillible-function**
- **box-constructor**
- **observe-address**
- **boxed-rfl-mutex**
- **asahi-monster-struct**

## See also

- https://github.com/rust-lang/beyond-refs/blob/main/src/in-place-init.md#potential-design-axioms
- https://rust-lang.zulipchat.com/#narrow/channel/528918-t-lang.2Fin-place-init/topic/in-place.20initialization.3A.20RfL.20design.20wishes/with/539083811
