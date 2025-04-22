# Benchmark

It uses YT table dump file as input. See the `data` subdirectory for an example.

Example:
```
$ ./benchmark data/company_shard.yson
```

Steps:
* create the WAD file (measuring the write time);
* print its size;
* scan the WAD file;
* check that the written and read data have the same CRC32.
