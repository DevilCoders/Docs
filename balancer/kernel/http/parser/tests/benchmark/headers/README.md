# Результаты бенчмарка

```
ya make -r && ./headers
```

```
--------------------------------------------------------------------------------------------
Benchmark                                                  Time             CPU   Iterations
--------------------------------------------------------------------------------------------
BMAddStringAndString                              4471 ns         4455 ns       620705
BMAddStaticStringAndStaticString                  2950 ns         2950 ns       953825
BMAddStringAndStringStorage                       4754 ns         4771 ns       589212
BMAddStringStorageAndStringStorage                5213 ns         5240 ns       535938
BMAddNonOwningStringBufAndStringBuf               3246 ns         3251 ns       841250
BMAddNonOwningStringAndStringStorage              4020 ns         4024 ns       692394
BMAddNonOwningStringStorageAndStringStorage       3793 ns         3796 ns       736871
BMFindValues                                            1968 ns         1972 ns      1429151
```
