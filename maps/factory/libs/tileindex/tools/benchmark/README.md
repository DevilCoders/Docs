# Benchmark output

```text
Size: 8388608 bytes, compressed size: 1860105 bytes, compression ratio: 22.17417955%
----------- New_tile_range ---------------
 samples:       63
 iterations:    2556
 iterations hr:    2.56K
 run time:      5.008008227
 per iteration: 4019458.604 (4.02M) cycles
----------- New_atomic_tile_range ---------------
 samples:       24
 iterations:    378
 iterations hr:    378
 run time:      5.045075884
 per iteration: 29034306.45 (29M) cycles
----------- Old_tile_range ---------------
 samples:       56
 iterations:    2016
 iterations hr:    2.02K
 run time:      5.114990506
 per iteration: 5565234.548 (5.57M) cycles
----------- Decompress_std_copy ---------------
 samples:       86
 iterations:    4656
 iterations hr:    4.66K
 run time:      5.010204196
 per iteration: 2352124.128 (2.35M) cycles
----------- Decompress ---------------
 samples:       38
 iterations:    946
 iterations hr:    946
 run time:      5.006041444
 per iteration: 11481207.61 (11.5M) cycles
```
