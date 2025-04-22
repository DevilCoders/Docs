# Monadic operations for `TMaybe`

## Usage

Expression `Map(m, f)` is almost equivalent to this code snippet:
```
m ? MakeMaybe<decltype(f(m))>(f(m)) : Nothing()
```

## Why this library exists?

There is proposal `P0798` "Monadic operations for std::optional".
It proposes 3 new member functions for `std::optional`:
* `transform` (aka `map`)
* `and_then`
* `or_else`

Current revision is [p0798](http://www.open-std.org/jtc1/sc22/wg21/docs/papers/2019/p0798r4.html). It wasn't adopted for C++20, but looks like work continues. You can follow it on the [issue on github](https://github.com/cplusplus/papers/issues/112).

We have our [internal task](https://st.yandex-team.ru/IGNIETFERRO-818) about adding the same operations as member functions of `TMaybe` but it's stalling.

So I added free function implementation as temporary solution.
