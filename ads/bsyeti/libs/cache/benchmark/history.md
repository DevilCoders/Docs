### 07.07.2022 (RemoveIfNeed up to 2 items in Update)
```
-------------------------------------------------------------------------------------------------------
Benchmark                                             Time             CPU   Iterations UserCounters...
-------------------------------------------------------------------------------------------------------
TCacheFixture/CacheTest/real_time/threads:10  307243972 ns    208241395 ns           10 size=10k
TCacheFixture/CacheTest/real_time/threads:16  211295021 ns    132740915 ns           16 size=10k
TCacheFixture/CacheTest/real_time/threads:30  234228956 ns    109766897 ns           30 size=10k
```

### 16.03.2021 (Aligned by cacheline)
```
-------------------------------------------------------------------------------------------------------
Benchmark                                             Time             CPU   Iterations UserCounters...
-------------------------------------------------------------------------------------------------------
TCacheFixture/CacheTest/real_time/threads:10  273028928 ns    265445697 ns           10 size=10k
TCacheFixture/CacheTest/real_time/threads:16  240162623 ns    232407437 ns           16 size=10k
TCacheFixture/CacheTest/real_time/threads:30  192974160 ns    176453725 ns           30 size=10k
```

### 13.03.2021 (Concurrent cache implementation)
```
-------------------------------------------------------------------------------------------------------
Benchmark                                             Time             CPU   Iterations UserCounters...
-------------------------------------------------------------------------------------------------------
TCacheFixture/CacheTest/real_time/threads:10  300218659 ns    290005769 ns           10 size=10k
TCacheFixture/CacheTest/real_time/threads:16  261214225 ns    254148538 ns           16 size=10k
TCacheFixture/CacheTest/real_time/threads:30  225420041 ns    207661164 ns           30 size=10k
```

### 12.03.2021 (Initial)

```
-------------------------------------------------------------------------------------------------------
Benchmark                                             Time             CPU   Iterations UserCounters...
-------------------------------------------------------------------------------------------------------
TCacheFixture/CacheTest/real_time/threads:10  428597782 ns    395861563 ns           10 size=15.1037M
TCacheFixture/CacheTest/real_time/threads:16  350060311 ns    322855363 ns           16 size=19.4634M
TCacheFixture/CacheTest/real_time/threads:30  309142572 ns    288047646 ns           30 size=21.8857M
```
