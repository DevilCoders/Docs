### 16.12.21 (Viewer for yabs)
-----------------------------------------------------------------------------------
Benchmark                                         Time             CPU   Iterations
-----------------------------------------------------------------------------------
```
...
BM_ViewerLookUp<TBigbViewer>/1               163207 ns       163204 ns         3613
BM_ViewerLookUp<TBigbViewer>/11               64647 ns        64595 ns        12221
BM_ViewerLookUp<TBigbViewer>/21               48201 ns        48178 ns        12619
BM_ViewerLookUp<TBigbViewer>/31               46212 ns        46205 ns        14659
BM_ViewerLookUp<TBigbViewer>/41               51305 ns        51152 ns        15512
BM_ViewerLookUp<TBigbViewer>/51               48348 ns        48346 ns        14398
BM_ViewerLookUp<TBigbViewer>/61               49203 ns        49198 ns        13653
BM_ViewerLookUp<TBigbViewer>/71               49828 ns        49826 ns        13406
BM_ViewerLookUp<TBigbViewer>/81               48822 ns        48816 ns        14717
BM_ViewerLookUp<TBigbViewer>/91               48443 ns        48441 ns        13599
BM_ViewerLookUp<TBigbViewer>_BigO            774.92 N        774.62 N
BM_ViewerLookUp<TBigbViewer>_RMS                 92 %            92 %
BM_ViewerLookUp<TYabsViewer>/1               228715 ns       228710 ns         3498
BM_ViewerLookUp<TYabsViewer>/11               59015 ns        59014 ns        11453
BM_ViewerLookUp<TYabsViewer>/21               48556 ns        48554 ns        14522
BM_ViewerLookUp<TYabsViewer>/31               49513 ns        49512 ns        14629
BM_ViewerLookUp<TYabsViewer>/41               45494 ns        45493 ns        15470
BM_ViewerLookUp<TYabsViewer>/51               43477 ns        43473 ns        15684
BM_ViewerLookUp<TYabsViewer>/61               46053 ns        46049 ns        15600
BM_ViewerLookUp<TYabsViewer>/71               42566 ns        42564 ns        15916
BM_ViewerLookUp<TYabsViewer>/81               40868 ns        40866 ns        15344
BM_ViewerLookUp<TYabsViewer>/91               38599 ns        38599 ns        16726
BM_ViewerLookUp<TYabsViewer>_BigO            685.80 N        685.77 N
BM_ViewerLookUp<TYabsViewer>_RMS                118 %           118 %
BM_ViewerPrepare<TBigbViewer>                  2.65 ns         2.65 ns    256750530
BM_ViewerPrepare<TYabsViewer>                101519 ns       101516 ns         6734
BM_ViewerOneKey<TBigbViewer>                  10140 ns        10140 ns        71321
BM_ViewerOneKey<TYabsViewer>                   6627 ns         6627 ns       103296
BM_ViewerBuildAndOneKey<TBigbViewer>          24177 ns        24176 ns        28703
BM_ViewerBuildAndOneKey<TYabsViewer>         116113 ns       116111 ns         5868
BM_ViewerBuildAndOneKeyMiss<TBigbViewer>      22509 ns        22509 ns        30534
BM_ViewerBuildAndOneKeyMiss<TYabsViewer>     127610 ns       127605 ns         6002
BM_ViewerCheck<TYabsViewer>                  489759 ns       489743 ns         1464
```

### 02.09.21 (Add fast update)
---------------------------------------------------------------------------------------
Benchmark                                             Time             CPU   Iterations
---------------------------------------------------------------------------------------
```
...
BM_Preload<TMutableCounters>/10                   79145 ns        79080 ns         8298
BM_Preload<TMutableCounters>/74                  144016 ns       143887 ns         4813
BM_Preload<TMutableCounters>/138                 148498 ns       148363 ns         4771
BM_Preload<TMutableCounters>/202                 153980 ns       153807 ns         4717
BM_Preload<TMutableCounters>/266                 154405 ns       154253 ns         4640
BM_Preload<TMutableCounters>_BigO                764.56 N        763.79 N
BM_Preload<TMutableCounters>_RMS                     43 %            43 %
BM_Insert<EUpdateWay::Fast>/10                   361804 ns       361329 ns         2004
BM_Insert<EUpdateWay::Fast>/74                   803016 ns       801822 ns          952
BM_Insert<EUpdateWay::Fast>/138                  752912 ns       751964 ns          926
BM_Insert<EUpdateWay::Fast>/202                  726564 ns       725868 ns          959
BM_Insert<EUpdateWay::Fast>/266                  755919 ns       755078 ns          806
BM_Insert<EUpdateWay::Fast>_BigO                3780.17 N       3775.85 N
BM_Insert<EUpdateWay::Fast>_RMS                      46 %            46 %
BM_Insert<EUpdateWay::Old>/10                    404375 ns       403990 ns         1687
BM_Insert<EUpdateWay::Old>/74                    868589 ns       868294 ns          807
BM_Insert<EUpdateWay::Old>/138                   846580 ns       846553 ns          851
BM_Insert<EUpdateWay::Old>/202                   938850 ns       938805 ns          850
BM_Insert<EUpdateWay::Old>/266                   872035 ns       872004 ns          795
BM_Insert<EUpdateWay::Old>_BigO                 4455.55 N       4455.20 N
BM_Insert<EUpdateWay::Old>_RMS                       43 %            43 %
BM_InsertManyKeys<EUpdateWay::Fast>/10           147149 ns       147144 ns         4819
BM_InsertManyKeys<EUpdateWay::Fast>/74          1058454 ns      1058421 ns          653
BM_InsertManyKeys<EUpdateWay::Fast>/138         1902354 ns      1902317 ns          330
BM_InsertManyKeys<EUpdateWay::Fast>/202         2888021 ns      2887965 ns          234
BM_InsertManyKeys<EUpdateWay::Fast>/266         3797359 ns      3797169 ns          177
BM_InsertManyKeys<EUpdateWay::Fast>_BigO       14215.01 N      14214.50 N
BM_InsertManyKeys<EUpdateWay::Fast>_RMS               1 %             1 %
BM_InsertManyKeys<EUpdateWay::Old>/10            176887 ns       176879 ns         3811
BM_InsertManyKeys<EUpdateWay::Old>/74           1324407 ns      1324395 ns          523
BM_InsertManyKeys<EUpdateWay::Old>/138          2346878 ns      2346831 ns          304
BM_InsertManyKeys<EUpdateWay::Old>/202          3479325 ns      3479255 ns          194
BM_InsertManyKeys<EUpdateWay::Old>/266          4415714 ns      4415569 ns          151
BM_InsertManyKeys<EUpdateWay::Old>_BigO        16897.10 N      16896.66 N
BM_InsertManyKeys<EUpdateWay::Old>_RMS                2 %             2 %
BM_InsertWithRepetition<EUpdateWay::Fast>/1      797147 ns       797140 ns          855
BM_InsertWithRepetition<EUpdateWay::Fast>/5     2957165 ns      2957068 ns          223
BM_InsertWithRepetition<EUpdateWay::Fast>/9     5623550 ns      5623499 ns          123
BM_InsertWithRepetition<EUpdateWay::Fast>/13    8448394 ns      8448016 ns           86
BM_InsertWithRepetition<EUpdateWay::Fast>/17   11055317 ns     11054968 ns           62
BM_InsertWithRepetition<EUpdateWay::Fast>/21   12924251 ns     12923726 ns           54
BM_InsertWithRepetition<EUpdateWay::Fast>/25   16495832 ns     16495464 ns           42
BM_InsertWithRepetition<EUpdateWay::Fast>/29   17864872 ns     17864244 ns           38
BM_InsertWithRepetition<EUpdateWay::Fast>_BigO  633434.78 N     633414.47 N
BM_InsertWithRepetition<EUpdateWay::Fast>_RMS          4 %             4 %
BM_InsertWithRepetition<EUpdateWay::Old>/1       781576 ns       781570 ns          875
BM_InsertWithRepetition<EUpdateWay::Old>/5      3295442 ns      3295410 ns          219
BM_InsertWithRepetition<EUpdateWay::Old>/9      6264967 ns      6264908 ns          113
BM_InsertWithRepetition<EUpdateWay::Old>/13     9572499 ns      9572168 ns           76
BM_InsertWithRepetition<EUpdateWay::Old>/17    12458095 ns     12457852 ns           52
BM_InsertWithRepetition<EUpdateWay::Old>/21    15163958 ns     15162997 ns           46
BM_InsertWithRepetition<EUpdateWay::Old>/25    17985599 ns     17985250 ns           40
BM_InsertWithRepetition<EUpdateWay::Old>/29    20322567 ns     20322156 ns           32
BM_InsertWithRepetition<EUpdateWay::Old>_BigO  714931.69 N     714911.49 N
BM_InsertWithRepetition<EUpdateWay::Old>_RMS          2 %             2 %
BM_Cleanup<TMutableCounters>/1                   765111 ns       765104 ns          877
BM_Cleanup<TMutableCounters>/5                  3428869 ns      3428791 ns          204
BM_Cleanup<TMutableCounters>/9                  6838218 ns      6838153 ns          110
BM_Cleanup<TMutableCounters>/13                10856009 ns     10855800 ns           70
BM_Cleanup<TMutableCounters>/17                14095737 ns     14095491 ns           52
BM_Cleanup<TMutableCounters>/21                17170928 ns     17170606 ns           41
BM_Cleanup<TMutableCounters>/25                19590335 ns     19589619 ns           35
BM_Cleanup<TMutableCounters>/29                21977229 ns     21976790 ns           30
BM_Cleanup<TMutableCounters>_BigO             787984.04 N     787965.74 N
BM_Cleanup<TMutableCounters>_RMS                      5 %             5 %
BM_Find<TMutableCounters>/10                      55295 ns        55294 ns        12724
BM_Find<TMutableCounters>/74                     133379 ns       133376 ns         5157
BM_Find<TMutableCounters>/138                    139801 ns       139798 ns         5267
BM_Find<TMutableCounters>/202                    136813 ns       136807 ns         5186
BM_Find<TMutableCounters>/266                    141822 ns       141819 ns         4986
BM_Find<TMutableCounters>_BigO                   698.17 N        698.15 N
BM_Find<TMutableCounters>_RMS                        42 %            42 %
```

### 12.07.21 (Changed time getter)
**стало**
```
...
---------------------------------------------------------------------------------------
Benchmark                                             Time             CPU   Iterations
---------------------------------------------------------------------------------------
BM_Preload<TMutableCounters>/10                   86544 ns        86523 ns         8162
BM_Preload<TMutableCounters>/74                  154613 ns       154585 ns         4457
BM_Preload<TMutableCounters>/138                 161902 ns       161859 ns         3969
BM_Preload<TMutableCounters>/202                 164511 ns       164477 ns         4425
BM_Preload<TMutableCounters>/266                 174756 ns       174716 ns         3850
BM_Preload<TMutableCounters>_BigO                839.81 N        839.62 N
BM_Preload<TMutableCounters>_RMS                     42 %            42 %
BM_Insert<TMutableCounters>/10                   436934 ns       436842 ns         1606
BM_Insert<TMutableCounters>/74                   892926 ns       892705 ns          763
BM_Insert<TMutableCounters>/138                  913533 ns       913318 ns          752
BM_Insert<TMutableCounters>/202                  986966 ns       986747 ns          778
BM_Insert<TMutableCounters>/266                  933730 ns       933512 ns          682
BM_Insert<TMutableCounters>_BigO                4730.89 N       4729.80 N
BM_Insert<TMutableCounters>_RMS                      42 %            42 %
BM_InsertWithRepetition<TMutableCounters>/1      752703 ns       752591 ns          943
BM_InsertWithRepetition<TMutableCounters>/5     3424738 ns      3423909 ns          215
BM_InsertWithRepetition<TMutableCounters>/9     6580382 ns      6578792 ns          111
BM_InsertWithRepetition<TMutableCounters>/13    9224500 ns      9222633 ns           69
BM_InsertWithRepetition<TMutableCounters>/17   13721484 ns     13717893 ns           52
BM_InsertWithRepetition<TMutableCounters>/21   17143113 ns     17137345 ns           42
BM_InsertWithRepetition<TMutableCounters>/25   19259235 ns     19254348 ns           37
BM_InsertWithRepetition<TMutableCounters>/29   20456791 ns     20452571 ns           30
BM_InsertWithRepetition<TMutableCounters>_BigO  754456.62 N     754266.66 N
BM_InsertWithRepetition<TMutableCounters>_RMS          7 %             7 %
BM_Cleanup<TMutableCounters>/1                   825741 ns       825267 ns          918
BM_Cleanup<TMutableCounters>/5                  3659808 ns      3659732 ns          202
BM_Cleanup<TMutableCounters>/9                  6986986 ns      6986583 ns           85
BM_Cleanup<TMutableCounters>/13                10465150 ns     10464807 ns           69
BM_Cleanup<TMutableCounters>/17                14421215 ns     14420749 ns           51
BM_Cleanup<TMutableCounters>/21                17401051 ns     17400203 ns           39
BM_Cleanup<TMutableCounters>/25                19782021 ns     19781638 ns           35
BM_Cleanup<TMutableCounters>/29                24563528 ns     24561955 ns           31
BM_Cleanup<TMutableCounters>_BigO             823434.55 N     823398.19 N
BM_Cleanup<TMutableCounters>_RMS                      4 %             4 %
BM_Find<TMutableCounters>/10                      56188 ns        56187 ns        12262
BM_Find<TMutableCounters>/74                     140942 ns       140937 ns         5259
BM_Find<TMutableCounters>/138                    143775 ns       143767 ns         4858
BM_Find<TMutableCounters>/202                    133951 ns       133927 ns         5308
BM_Find<TMutableCounters>/266                    141466 ns       141426 ns         5042
BM_Find<TMutableCounters>_BigO                   701.43 N        701.30 N
BM_Find<TMutableCounters>_RMS                        44 %            44 %
```

**было**
```
...
---------------------------------------------------------------------------------------
Benchmark                                             Time             CPU   Iterations
---------------------------------------------------------------------------------------
BM_Preload<TMutableCounters>/10                  101879 ns       101869 ns         7254
BM_Preload<TMutableCounters>/74                  160263 ns       160240 ns         4430
BM_Preload<TMutableCounters>/138                 178459 ns       178435 ns         4150
BM_Preload<TMutableCounters>/202                 174192 ns       174166 ns         3891
BM_Preload<TMutableCounters>/266                 172902 ns       172883 ns         3499
BM_Preload<TMutableCounters>_BigO                871.52 N        871.41 N
BM_Preload<TMutableCounters>_RMS                     45 %            45 %
BM_Insert<TMutableCounters>/10                   431302 ns       431227 ns         1661
BM_Insert<TMutableCounters>/74                   985415 ns       985330 ns          783
BM_Insert<TMutableCounters>/138                  899229 ns       899221 ns          676
BM_Insert<TMutableCounters>/202                  920517 ns       920428 ns          721
BM_Insert<TMutableCounters>/266                  994766 ns       994711 ns          739
BM_Insert<TMutableCounters>_BigO                4786.90 N       4786.60 N
BM_Insert<TMutableCounters>_RMS                      44 %            44 %
BM_InsertWithRepetition<TMutableCounters>/1      787721 ns       787682 ns          864
BM_InsertWithRepetition<TMutableCounters>/5     3697775 ns      3697633 ns          192
BM_InsertWithRepetition<TMutableCounters>/9     6742308 ns      6742004 ns           95
BM_InsertWithRepetition<TMutableCounters>/13   10198695 ns     10198284 ns           70
BM_InsertWithRepetition<TMutableCounters>/17   14580416 ns     14580122 ns           53
BM_InsertWithRepetition<TMutableCounters>/21   16316790 ns     16316652 ns           37
BM_InsertWithRepetition<TMutableCounters>/25   18350286 ns     18348600 ns           37
BM_InsertWithRepetition<TMutableCounters>/29   24615606 ns     24610119 ns           35
BM_InsertWithRepetition<TMutableCounters>_BigO  799219.16 N     799130.99 N
BM_InsertWithRepetition<TMutableCounters>_RMS          7 %             7 %
BM_Cleanup<TMutableCounters>/1                   859793 ns       859776 ns          876
BM_Cleanup<TMutableCounters>/5                  3822980 ns      3822944 ns          180
BM_Cleanup<TMutableCounters>/9                  7282074 ns      7281918 ns          101
BM_Cleanup<TMutableCounters>/13                10506401 ns     10505969 ns           67
BM_Cleanup<TMutableCounters>/17                14630702 ns     14630378 ns           48
BM_Cleanup<TMutableCounters>/21                16955162 ns     16954751 ns           36
BM_Cleanup<TMutableCounters>/25                23019476 ns     23018974 ns           31
BM_Cleanup<TMutableCounters>/29                26705435 ns     26702799 ns           24
BM_Cleanup<TMutableCounters>_BigO             880591.19 N     880546.54 N
BM_Cleanup<TMutableCounters>_RMS                      7 %             7 %
BM_Find<TMutableCounters>/10                      63091 ns        63090 ns        11214
BM_Find<TMutableCounters>/74                     148175 ns       148173 ns         4667
BM_Find<TMutableCounters>/138                    151386 ns       151380 ns         4656
BM_Find<TMutableCounters>/202                    144314 ns       144310 ns         4857
BM_Find<TMutableCounters>/266                    150277 ns       150272 ns         4867
BM_Find<TMutableCounters>_BigO                   746.16 N        746.14 N
BM_Find<TMutableCounters>_RMS                        44 %            44 %
```


### 18.06.21 (Changed map for pack index)
**стало**
```
...
---------------------------------------------------------------------------------------
Benchmark                                             Time             CPU   Iterations
---------------------------------------------------------------------------------------
BM_Preload<TMutableCounters>/10                   93085 ns        93084 ns         7997
BM_Preload<TMutableCounters>/74                  163448 ns       163444 ns         4670
BM_Preload<TMutableCounters>/138                 163105 ns       163103 ns         3839
BM_Preload<TMutableCounters>/202                 162696 ns       162694 ns         4513
BM_Preload<TMutableCounters>/266                 163658 ns       163654 ns         4175
BM_Preload<TMutableCounters>_BigO                821.94 N        821.93 N
BM_Preload<TMutableCounters>_RMS                     46 %            46 %
BM_Insert<TMutableCounters>/10                   416698 ns       416694 ns         1597
BM_Insert<TMutableCounters>/74                   867242 ns       867234 ns          844
BM_Insert<TMutableCounters>/138                  903912 ns       903896 ns          758
BM_Insert<TMutableCounters>/202                 1005266 ns      1005203 ns          705
BM_Insert<TMutableCounters>/266                  887200 ns       887179 ns          744
BM_Insert<TMutableCounters>_BigO                4641.96 N       4641.80 N
BM_Insert<TMutableCounters>_RMS                      43 %            43 %
BM_InsertWithRepetition<TMutableCounters>/1      728709 ns       728695 ns          907
BM_InsertWithRepetition<TMutableCounters>/5     3168599 ns      3168527 ns          230
BM_InsertWithRepetition<TMutableCounters>/9     6003302 ns      6003254 ns          120
BM_InsertWithRepetition<TMutableCounters>/13    9479615 ns      9479395 ns           77
BM_InsertWithRepetition<TMutableCounters>/17   12490158 ns     12489900 ns           54
BM_InsertWithRepetition<TMutableCounters>/21   16362863 ns     16362503 ns           45
BM_InsertWithRepetition<TMutableCounters>/25   18014570 ns     18014229 ns           40
BM_InsertWithRepetition<TMutableCounters>/29   19957605 ns     19956461 ns           30
BM_InsertWithRepetition<TMutableCounters>_BigO  719629.46 N     719606.27 N
BM_InsertWithRepetition<TMutableCounters>_RMS          6 %             6 %
BM_Cleanup<TMutableCounters>/1                   747265 ns       747250 ns          938
BM_Cleanup<TMutableCounters>/5                  3403467 ns      3403392 ns          204
BM_Cleanup<TMutableCounters>/9                  6410991 ns      6410939 ns          110
BM_Cleanup<TMutableCounters>/13                 9882384 ns      9882295 ns           67
BM_Cleanup<TMutableCounters>/17                13765863 ns     13765472 ns           55
BM_Cleanup<TMutableCounters>/21                16349785 ns     16349458 ns           43
BM_Cleanup<TMutableCounters>/25                19989661 ns     19989293 ns           37
BM_Cleanup<TMutableCounters>/29                22571206 ns     22570820 ns           30
BM_Cleanup<TMutableCounters>_BigO             783012.21 N     782997.67 N
BM_Cleanup<TMutableCounters>_RMS                      3 %             3 %
BM_Find<TMutableCounters>/10                      52086 ns        52084 ns        12589
BM_Find<TMutableCounters>/74                     126885 ns       126882 ns         5382
BM_Find<TMutableCounters>/138                    134028 ns       134027 ns         5067
BM_Find<TMutableCounters>/202                    130324 ns       130323 ns         5486
BM_Find<TMutableCounters>/266                    132452 ns       132449 ns         5599
BM_Find<TMutableCounters>_BigO                   660.62 N        660.61 N
BM_Find<TMutableCounters>_RMS                        42 %            42 %
```

**было**
```
...
---------------------------------------------------------------------------------------
Benchmark                                             Time             CPU   Iterations
---------------------------------------------------------------------------------------
BM_Preload<TMutableCounters>/10                  133043 ns       133038 ns         5104
BM_Preload<TMutableCounters>/74                  301418 ns       301387 ns         2365
BM_Preload<TMutableCounters>/138                 324294 ns       324287 ns         2339
BM_Preload<TMutableCounters>/202                 328525 ns       328518 ns         2141
BM_Preload<TMutableCounters>/266                 348503 ns       347935 ns         1930
BM_Preload<TMutableCounters>_BigO               1670.23 N       1669.08 N
BM_Preload<TMutableCounters>_RMS                     39 %            39 %
BM_Insert<TMutableCounters>/10                   490093 ns       490071 ns         1407
BM_Insert<TMutableCounters>/74                  1140493 ns      1140442 ns          672
BM_Insert<TMutableCounters>/138                 1134885 ns      1134761 ns          605
BM_Insert<TMutableCounters>/202                 1080978 ns      1080923 ns          625
BM_Insert<TMutableCounters>/266                 1186992 ns      1186891 ns          618
BM_Insert<TMutableCounters>_BigO                5727.78 N       5727.35 N
BM_Insert<TMutableCounters>_RMS                      43 %            43 %
BM_InsertWithRepetition<TMutableCounters>/1      889962 ns       889903 ns          785
BM_InsertWithRepetition<TMutableCounters>/5     4028563 ns      4028343 ns          185
BM_InsertWithRepetition<TMutableCounters>/9     7598026 ns      7597772 ns           91
BM_InsertWithRepetition<TMutableCounters>/13   11365695 ns     11365240 ns           57
BM_InsertWithRepetition<TMutableCounters>/17   17421750 ns     17420803 ns           44
BM_InsertWithRepetition<TMutableCounters>/21   24483284 ns     24482755 ns           27
BM_InsertWithRepetition<TMutableCounters>/25   26930072 ns     26929066 ns           23
BM_InsertWithRepetition<TMutableCounters>/29   30690637 ns     30689993 ns           21
BM_InsertWithRepetition<TMutableCounters>_BigO 1056135.93 N    1056103.42 N
BM_InsertWithRepetition<TMutableCounters>_RMS          9 %             9 %
BM_Cleanup<TMutableCounters>/1                   913684 ns       913645 ns          772
BM_Cleanup<TMutableCounters>/5                  4226421 ns      4226241 ns          180
BM_Cleanup<TMutableCounters>/9                  8535625 ns      8535356 ns           87
BM_Cleanup<TMutableCounters>/13                13280427 ns     13279645 ns           55
BM_Cleanup<TMutableCounters>/17                18117923 ns     18116845 ns           39
BM_Cleanup<TMutableCounters>/21                23504078 ns     23503318 ns           31
BM_Cleanup<TMutableCounters>/25                27479311 ns     27478132 ns           28
BM_Cleanup<TMutableCounters>/29                32849923 ns     32848385 ns           21
BM_Cleanup<TMutableCounters>_BigO            1097383.84 N    1097334.52 N
BM_Cleanup<TMutableCounters>_RMS                      5 %             5 %
BM_Find<TMutableCounters>/10                      60489 ns        60486 ns        10729
BM_Find<TMutableCounters>/74                     159544 ns       159538 ns         4483
BM_Find<TMutableCounters>/138                    167300 ns       167293 ns         4324
BM_Find<TMutableCounters>/202                    161175 ns       161170 ns         4100
BM_Find<TMutableCounters>/266                    166627 ns       166616 ns         4459
BM_Find<TMutableCounters>_BigO                   825.22 N        825.18 N
BM_Find<TMutableCounters>_RMS                        42 %            42 %
```



### 08.03.21 (Global stats)

**стало**
```
...
BM_Cleanup<TMutableCounters>/1                   856680 ns       856308 ns          835
BM_Cleanup<TMutableCounters>/5                  3729586 ns      3727367 ns          189
BM_Cleanup<TMutableCounters>/9                  7802416 ns      7797129 ns           88
BM_Cleanup<TMutableCounters>/13                12242285 ns     12233250 ns           58
BM_Cleanup<TMutableCounters>/17                16256227 ns     16245217 ns           44
BM_Cleanup<TMutableCounters>/21                20458561 ns     20444830 ns           34
BM_Cleanup<TMutableCounters>/25                23848988 ns     23832832 ns           27
BM_Cleanup<TMutableCounters>/29                27878758 ns     27859482 ns           25
BM_Cleanup<TMutableCounters>_BigO             954518.76 N     953865.48 N
BM_Cleanup<TMutableCounters>_RMS                      3 %             3 %
```

**было**
```
...
BM_Cleanup<TMutableCounters>/1                   843664 ns       843660 ns          840
BM_Cleanup<TMutableCounters>/5                  3869998 ns      3869984 ns          180
BM_Cleanup<TMutableCounters>/9                  8334978 ns      8334842 ns           82
BM_Cleanup<TMutableCounters>/13                12973738 ns     12973532 ns           53
BM_Cleanup<TMutableCounters>/17                17014471 ns     17013922 ns           40
BM_Cleanup<TMutableCounters>/21                22815425 ns     22815077 ns           31
BM_Cleanup<TMutableCounters>/25                25079631 ns     25079212 ns           27
BM_Cleanup<TMutableCounters>/29                31258522 ns     31257998 ns           23
BM_Cleanup<TMutableCounters>_BigO            1037914.61 N    1037895.87 N
BM_Cleanup<TMutableCounters>_RMS                      6 %             6 %
```

### 25.03.21 (Added stats)

```
---------------------------------------------------------------------------------------
Benchmark                                             Time             CPU   Iterations
---------------------------------------------------------------------------------------
BM_Preload<TCounterMap>/10                       221954 ns       221943 ns         3151
BM_Preload<TCounterMap>/74                       591731 ns       591706 ns         1222
BM_Preload<TCounterMap>/138                      626667 ns       626663 ns         1143
BM_Preload<TCounterMap>/202                      638479 ns       638475 ns         1111
BM_Preload<TCounterMap>/266                      660609 ns       660592 ns         1053
BM_Preload<TCounterMap>_BigO                    3210.33 N       3210.27 N    
BM_Preload<TCounterMap>_RMS                          39 %            39 %    
BM_Preload<TMutableCounters>/10                  122141 ns       122137 ns         5802
BM_Preload<TMutableCounters>/74                  271382 ns       270880 ns         2607
BM_Preload<TMutableCounters>/138                 281486 ns       281246 ns         2529
BM_Preload<TMutableCounters>/202                 292656 ns       292397 ns         2420
BM_Preload<TMutableCounters>/266                 301641 ns       301496 ns         2396
BM_Preload<TMutableCounters>_BigO               1464.99 N       1463.80 N    
BM_Preload<TMutableCounters>_RMS                     40 %            40 %    
BM_Insert<TCounterMap>/10                        593261 ns       593016 ns         1196
BM_Insert<TCounterMap>/74                       1611074 ns      1609855 ns          388
BM_Insert<TCounterMap>/138                      1497889 ns      1497091 ns          471
BM_Insert<TCounterMap>/202                      1486134 ns      1485427 ns          471
BM_Insert<TCounterMap>/266                      1488773 ns      1488074 ns          472
BM_Insert<TCounterMap>_BigO                     7549.37 N       7545.47 N    
BM_Insert<TCounterMap>_RMS                           46 %            46 %    
BM_Insert<TMutableCounters>/10                   451954 ns       451758 ns         1548
BM_Insert<TMutableCounters>/74                   976181 ns       975733 ns          716
BM_Insert<TMutableCounters>/138                  987725 ns       987166 ns          694
BM_Insert<TMutableCounters>/202                  992540 ns       991994 ns          709
BM_Insert<TMutableCounters>/266                  985942 ns       985622 ns          711
BM_Insert<TMutableCounters>_BigO                4962.67 N       4960.41 N    
BM_Insert<TMutableCounters>_RMS                      44 %            44 %    
BM_InsertWithRepetition<TCounterMap>/1           726979 ns       726792 ns          961
BM_InsertWithRepetition<TCounterMap>/5          6345602 ns      6340652 ns          108
BM_InsertWithRepetition<TCounterMap>/9         15297314 ns     15288894 ns           46
BM_InsertWithRepetition<TCounterMap>/13        25728848 ns     25711835 ns           27
BM_InsertWithRepetition<TCounterMap>/17        38308689 ns     38284639 ns           18
BM_InsertWithRepetition<TCounterMap>/21        51721123 ns     51687226 ns           10
BM_InsertWithRepetition<TCounterMap>/25        67172080 ns     67151731 ns           11
BM_InsertWithRepetition<TCounterMap>/29        82655556 ns     82653234 ns            8
BM_InsertWithRepetition<TCounterMap>_BigO    2555950.75 N    2555134.15 N    
BM_InsertWithRepetition<TCounterMap>_RMS             16 %            16 %    
BM_InsertWithRepetition<TMutableCounters>/1      658655 ns       658644 ns         1046
BM_InsertWithRepetition<TMutableCounters>/5     3080049 ns      3079960 ns          225
BM_InsertWithRepetition<TMutableCounters>/9     6336763 ns      6336660 ns          110
BM_InsertWithRepetition<TMutableCounters>/13   10102109 ns     10101930 ns           70
BM_InsertWithRepetition<TMutableCounters>/17   14257293 ns     14256778 ns           50
BM_InsertWithRepetition<TMutableCounters>/21   18202564 ns     18202033 ns           38
BM_InsertWithRepetition<TMutableCounters>/25   22239767 ns     22239160 ns           31
BM_InsertWithRepetition<TMutableCounters>/29   27178009 ns     27176877 ns           25
BM_InsertWithRepetition<TMutableCounters>_BigO  879126.80 N     879097.83 N    
BM_InsertWithRepetition<TMutableCounters>_RMS          9 %             9 %    
BM_Cleanup<TCounterMap>/1                        940075 ns       940059 ns          749
BM_Cleanup<TCounterMap>/5                       8498005 ns      8497807 ns           83
BM_Cleanup<TCounterMap>/9                      21977767 ns     21977434 ns           32
BM_Cleanup<TCounterMap>/13                     37355528 ns     37354979 ns           19
BM_Cleanup<TCounterMap>/17                     59521153 ns     59518576 ns           13
BM_Cleanup<TCounterMap>/21                     77190401 ns     77189904 ns            9
BM_Cleanup<TCounterMap>/25                     84717638 ns     84713466 ns            8
BM_Cleanup<TCounterMap>/29                    103042005 ns    103039470 ns            7
BM_Cleanup<TCounterMap>_BigO                 3424704.29 N    3424605.91 N    
BM_Cleanup<TCounterMap>_RMS                          11 %            11 %    
BM_Cleanup<TMutableCounters>/1                   718955 ns       718942 ns          927
BM_Cleanup<TMutableCounters>/5                  3474473 ns      3474421 ns          198
BM_Cleanup<TMutableCounters>/9                  7492442 ns      7492327 ns           94
BM_Cleanup<TMutableCounters>/13                11865455 ns     11865200 ns           60
BM_Cleanup<TMutableCounters>/17                16244431 ns     16244327 ns           43
BM_Cleanup<TMutableCounters>/21                20701965 ns     20701821 ns           34
BM_Cleanup<TMutableCounters>/25                24232914 ns     24232499 ns           28
BM_Cleanup<TMutableCounters>/29                28695838 ns     28695211 ns           24
BM_Cleanup<TMutableCounters>_BigO             966291.65 N     966276.29 N    
BM_Cleanup<TMutableCounters>_RMS                      5 %             5 %    
BM_Find<TCounterMap>/10                          179071 ns       179070 ns         3924
BM_Find<TCounterMap>/74                          541678 ns       541668 ns         1313
BM_Find<TCounterMap>/138                         545492 ns       545484 ns         1288
BM_Find<TCounterMap>/202                         558490 ns       558481 ns         1277
BM_Find<TCounterMap>/266                         546187 ns       546177 ns         1286
BM_Find<TCounterMap>_BigO                       2755.57 N       2755.52 N    
BM_Find<TCounterMap>_RMS                             42 %            42 %    
BM_Find<TMutableCounters>/10                      58566 ns        58562 ns        11901
BM_Find<TMutableCounters>/74                     150555 ns       150552 ns         4633
BM_Find<TMutableCounters>/138                    151103 ns       151099 ns         4623
BM_Find<TMutableCounters>/202                    153129 ns       153125 ns         4579
BM_Find<TMutableCounters>/266                    152120 ns       152118 ns         4469
BM_Find<TMutableCounters>_BigO                   763.51 N        763.49 N    
BM_Find<TMutableCounters>_RMS                        43 %            43 %    
```

### 24.03.21 (Initial)

```
---------------------------------------------------------------------------------------
Benchmark                                             Time             CPU   Iterations
---------------------------------------------------------------------------------------
BM_Preload<TCounterMap>/10                       236339 ns       236328 ns         2941
BM_Preload<TCounterMap>/74                       609509 ns       609465 ns         1189
BM_Preload<TCounterMap>/138                      668191 ns       668174 ns         1027
BM_Preload<TCounterMap>/202                      681525 ns       681495 ns         1051
BM_Preload<TCounterMap>/266                      696549 ns       696501 ns         1018
BM_Preload<TCounterMap>_BigO                    3397.18 N       3397.00 N    
BM_Preload<TCounterMap>_RMS                          39 %            39 %    
BM_Preload<TMutableCounters>/10                  129918 ns       129915 ns         5371
BM_Preload<TMutableCounters>/74                  288360 ns       288351 ns         2383
BM_Preload<TMutableCounters>/138                 303826 ns       303824 ns         2312
BM_Preload<TMutableCounters>/202                 309459 ns       309419 ns         2291
BM_Preload<TMutableCounters>/266                 304094 ns       304028 ns         2302
BM_Preload<TMutableCounters>_BigO               1527.14 N       1526.94 N    
BM_Preload<TMutableCounters>_RMS                     42 %            42 %    
BM_Insert<TCounterMap>/10                        619041 ns       619020 ns         1151
BM_Insert<TCounterMap>/74                       1550360 ns      1550304 ns          444
BM_Insert<TCounterMap>/138                      1512049 ns      1512020 ns          453
BM_Insert<TCounterMap>/202                      1509628 ns      1509601 ns          462
BM_Insert<TCounterMap>/266                      1532476 ns      1532438 ns          465
BM_Insert<TCounterMap>_BigO                     7652.84 N       7652.66 N    
BM_Insert<TCounterMap>_RMS                           44 %            44 %    
BM_Insert<TMutableCounters>/10                   458714 ns       458705 ns         1534
BM_Insert<TMutableCounters>/74                  1041624 ns      1041604 ns          697
BM_Insert<TMutableCounters>/138                 1138769 ns      1138746 ns          661
BM_Insert<TMutableCounters>/202                 1105894 ns      1105841 ns          655
BM_Insert<TMutableCounters>/266                 1116655 ns      1116619 ns          653
BM_Insert<TMutableCounters>_BigO                5575.26 N       5575.07 N    
BM_Insert<TMutableCounters>_RMS                      42 %            42 %    
BM_InsertWithRepetition<TCounterMap>/1           746027 ns       746020 ns          948
BM_InsertWithRepetition<TCounterMap>/5          7120888 ns      7120822 ns           99
BM_InsertWithRepetition<TCounterMap>/9         16884211 ns     16883858 ns           42
BM_InsertWithRepetition<TCounterMap>/13        27292883 ns     27291899 ns           25
BM_InsertWithRepetition<TCounterMap>/17        43074647 ns     43074257 ns           17
BM_InsertWithRepetition<TCounterMap>/21        60328169 ns     60326963 ns           11
BM_InsertWithRepetition<TCounterMap>/25        75627799 ns     75625328 ns           10
BM_InsertWithRepetition<TCounterMap>/29        95595498 ns     95593761 ns            7
BM_InsertWithRepetition<TCounterMap>_BigO    2914741.43 N    2914676.53 N    
BM_InsertWithRepetition<TCounterMap>_RMS             18 %            18 %    
BM_InsertWithRepetition<TMutableCounters>/1      688873 ns       688857 ns         1009
BM_InsertWithRepetition<TMutableCounters>/5     3247431 ns      3247369 ns          215
BM_InsertWithRepetition<TMutableCounters>/9     6693603 ns      6693548 ns          106
BM_InsertWithRepetition<TMutableCounters>/13   11219804 ns     11219510 ns           60
BM_InsertWithRepetition<TMutableCounters>/17   15123244 ns     15122462 ns           47
BM_InsertWithRepetition<TMutableCounters>/21   23056707 ns     23056183 ns           30
BM_InsertWithRepetition<TMutableCounters>/25   27454328 ns     27453620 ns           25
BM_InsertWithRepetition<TMutableCounters>/29   30064533 ns     30063947 ns           23
BM_InsertWithRepetition<TMutableCounters>_BigO 1020445.62 N    1020419.87 N    
BM_InsertWithRepetition<TMutableCounters>_RMS         12 %            12 %    
BM_Cleanup<TCounterMap>/1                        996576 ns       996534 ns          712
BM_Cleanup<TCounterMap>/5                       9381688 ns      9381511 ns           75
BM_Cleanup<TCounterMap>/9                      23646327 ns     23645862 ns           29
BM_Cleanup<TCounterMap>/13                     39976253 ns     39975481 ns           18
BM_Cleanup<TCounterMap>/17                     56273867 ns     56272787 ns           12
BM_Cleanup<TCounterMap>/21                     79470703 ns     79468655 ns            9
BM_Cleanup<TCounterMap>/25                     95137747 ns     95136846 ns            7
BM_Cleanup<TCounterMap>/29                    120398660 ns    120392472 ns            6
BM_Cleanup<TCounterMap>_BigO                 3752410.43 N    3752297.76 N    
BM_Cleanup<TCounterMap>_RMS                          14 %            14 %    
BM_Cleanup<TMutableCounters>/1                   772061 ns       771935 ns          923
BM_Cleanup<TMutableCounters>/5                  3607413 ns      3607315 ns          191
BM_Cleanup<TMutableCounters>/9                  7664583 ns      7664449 ns           91
BM_Cleanup<TMutableCounters>/13                12342706 ns     12342478 ns           58
BM_Cleanup<TMutableCounters>/17                16884119 ns     16883805 ns           41
BM_Cleanup<TMutableCounters>/21                22343081 ns     22342877 ns           32
BM_Cleanup<TMutableCounters>/25                26025365 ns     26024717 ns           27
BM_Cleanup<TMutableCounters>/29                30534119 ns     30533526 ns           23
BM_Cleanup<TMutableCounters>_BigO            1027752.37 N    1027733.03 N    
BM_Cleanup<TMutableCounters>_RMS                      6 %             6 %    
BM_Find<TCounterMap>/10                          189783 ns       189781 ns         3702
BM_Find<TCounterMap>/74                          557108 ns       557103 ns         1219
BM_Find<TCounterMap>/138                         570862 ns       570844 ns         1254
BM_Find<TCounterMap>/202                         575698 ns       575686 ns         1197
BM_Find<TCounterMap>/266                         577453 ns       577442 ns         1189
BM_Find<TCounterMap>_BigO                       2877.05 N       2876.99 N    
BM_Find<TCounterMap>_RMS                             41 %            41 %    
BM_Find<TMutableCounters>/10                      60401 ns        60401 ns        11734
BM_Find<TMutableCounters>/74                     157104 ns       157100 ns         4476
BM_Find<TMutableCounters>/138                    157338 ns       157332 ns         4403
BM_Find<TMutableCounters>/202                    165637 ns       165634 ns         4259
BM_Find<TMutableCounters>/266                    156987 ns       156984 ns         4486
BM_Find<TMutableCounters>_BigO                   801.58 N        801.56 N    
BM_Find<TMutableCounters>_RMS                        43 %            43 %    
---------------------------------------------------------------------------------------
```


