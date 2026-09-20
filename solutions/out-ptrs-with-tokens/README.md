# Out pointers

**Note: There isn't really a canonical "out pointers" proposal. There is a list of similar proposals, and discussions about them can be pretty fluid.**

Examples in this folder follow the "initialization tokens" syntax that has been proposed, among other places, in [beyond-refs/src/in-place-init/uninit-ref.md](https://github.com/rust-lang/beyond-refs/blob/5e2b3de108a96c93adc594acd3165aaf5b78c81b/src/in-place-init/uninit-ref.md) in the [beyond-refs](https://github.com/rust-lang/beyond-refs) exploration repository.

Examples try to stick to the syntax originally proposed by @aapoalas and @dingxiangfei2009 in `uninit-ref.md`, except for one point: the document proposes two syntaxes for initializing fields and values (`=` or `<-`). Examples here will use `<-` for in-place initialization and `=` for setting trivially-movable values (e.g. integers).

Examples use `init<'_>` instead of `Initialized<'_>` as the token syntax, which matches Zulip discussion at the time I'm writing this.
