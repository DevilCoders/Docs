Find connected components on MR
===============================

### Usage

```bash
$ ./crypta/graph/mrcc/cli/mrcc --help
usage: mrcc [-h] -s SOURCE [-d DESTINATION] [-u U] [-v V] [-cid CID]
            [--max_iter MAX_ITER] [--vdata]

Find connected components on MR

optional arguments:
  -h, --help            show this help message and exit
  -s SOURCE, --source SOURCE
                        YT path to source table
  -d DESTINATION, --destination DESTINATION
                        YT path to destination table (if not set, equal to
                        source path)
  -u U                  Name of u-column in source table (default: u)
  -v V                  Name of v-column in source table (default: v)
  -cid CID              Name of connected component id column in destination
                        table (default: component_id)
  --max_iter MAX_ITER   Maximum number of iterations to get converged graph
                        (default: 15)
  --vdata               Keep v_data column in destination table
```

### Example

1. Export yt env variables

    ```bash
    18/08/20 14:28:35 mskorokhod@ms-nix ~/ya/hg/arcadia $ cat ~/.yt/export
    export YT_TOKEN=$(cat ~/.yt/token)
    export YQL_TOKEN=$(cat ~/.yql/token)
    export YT_PROXY=hahn.yt.yandex.net

    18/08/20 14:28:50 mskorokhod@ms-nix ~/ya/hg/arcadia $ source ~/.yt/export
    ```

2. Run mrcc cli

    #### Via YT

    Default

    ```bash
    $ ./crypta/graph/mrcc/cli/mrcc -s //home/crypta/team/mskorokhod/cc_graph -d //home/crypta/team/mskorokhod/cc_graph_res_yt -u c1 -v c2
    [INFO] 2018-08-21 21:53:25,914 :: Starting mrcc
    2018-08-21 21:54:58,571 INFO    Operation started: http://hahn.yt.yandex.net/?page=operation&mode=detail&id=efa7f324-176685cd-3fe03e8-c614ebd5&tab=details
    2018-08-21 21:54:58.827 (-1 min)    operation efa7f324-176685cd-3fe03e8-c614ebd5 starting
    2018-08-21 21:54:59.952 (-1 min)    operation efa7f324-176685cd-3fe03e8-c614ebd5 initializing
    2018-08-21 21:55:15.850 ( 0 min)    operation efa7f324-176685cd-3fe03e8-c614ebd5: running=0 completed=0 pending=125 failed=0    aborted=0   lost=0  total=125
    2018-08-21 21:56:15.958 ( 1 min)    operation efa7f324-176685cd-3fe03e8-c614ebd5: running=111   completed=21    pending=0   failed=0    aborted=12  lost=0  total=132
    2018-08-21 21:57:03.613 ( 1 min)    operation efa7f324-176685cd-3fe03e8-c614ebd5 completing
    2018-08-21 21:57:08.698 ( 1 min)    operation efa7f324-176685cd-3fe03e8-c614ebd5 completed
    [INFO] 2018-08-21 21:57:09,701 :: Starting iteration 1
    [INFO] 2018-08-21 22:06:40,927 :: Iteration 1 complete. Large star changes: 18245511. Small star changes: 26425753
    [INFO] 2018-08-21 22:06:40,928 :: Starting iteration 2
    [INFO] 2018-08-21 22:15:29,672 :: Iteration 2 complete. Large star changes: 2194000. Small star changes: 4186621
    [INFO] 2018-08-21 22:15:29,673 :: Starting iteration 3
    [INFO] 2018-08-21 22:24:01,446 :: Iteration 3 complete. Large star changes: 572553. Small star changes: 360531
    [INFO] 2018-08-21 22:24:01,446 :: Starting iteration 4
    [INFO] 2018-08-21 22:38:45,255 :: Iteration 4 complete. Large star changes: 62520. Small star changes: 11887
    [INFO] 2018-08-21 22:38:45,255 :: Starting iteration 5
    [INFO] 2018-08-21 22:56:15,668 :: Iteration 5 complete. Large star changes: 1135. Small star changes: 74
    [INFO] 2018-08-21 22:56:15,668 :: Starting iteration 6
    [INFO] 2018-08-21 23:04:25,633 :: Iteration 6 complete. Large star changes: 32. Small star changes: 2
    [INFO] 2018-08-21 23:04:25,633 :: Starting iteration 7
    [INFO] 2018-08-21 23:11:51,620 :: Iteration 7 complete. Large star changes: 2. Small star changes: 0
    [INFO] 2018-08-21 23:11:51,620 :: Starting iteration 8
    [INFO] 2018-08-21 23:18:58,757 :: Iteration 8 complete. Large star changes: 0. Small star changes: 0
    [INFO] 2018-08-21 23:18:58,757 :: Converged
    [INFO] 2018-08-21 23:18:58,925 :: Finishing mrcc
    2018-08-21 23:19:02,528 INFO    Operation started: http://hahn.yt.yandex.net/?page=operation&mode=detail&id=3645db4f-1bfddae3-3fe03e8-4475b37f&tab=details
    2018-08-21 23:19:02.583 (-1 min)    operation 3645db4f-1bfddae3-3fe03e8-4475b37f initializing
    2018-08-21 23:19:17.098 ( 0 min)    operation 3645db4f-1bfddae3-3fe03e8-4475b37f: running=0 completed=0 pending=12  failed=0    aborted=0   lost=0  total=12
    2018-08-21 23:20:15.676 ( 1 min)    operation 3645db4f-1bfddae3-3fe03e8-4475b37f completed
    2018-08-21 23:20:16,866 INFO    Operation started: http://hahn.yt.yandex.net/?page=operation&mode=detail&id=efbbc77f-a7130abe-3fe03e8-c853864&tab=details
    2018-08-21 23:20:16.941 (-1 min)    operation efbbc77f-a7130abe-3fe03e8-c853864 starting
    2018-08-21 23:20:18.033 (-1 min)    operation efbbc77f-a7130abe-3fe03e8-c853864 initializing
    2018-08-21 23:20:29.958 ( 0 min)    operation efbbc77f-a7130abe-3fe03e8-c853864: running=0  completed=0 pending=28  failed=0    aborted=0   lost=0  total=28
    2018-08-21 23:21:25.749 ( 0 min)    operation efbbc77f-a7130abe-3fe03e8-c853864: running=0  completed=23    pending=6   failed=0    aborted=1   lost=0  total=29
    2018-08-21 23:22:18.363 ( 1 min)    operation efbbc77f-a7130abe-3fe03e8-c853864 completed
    ```

    #### Via YQL

    Flag `--yql`

    ```bash
    $ ./crypta/graph/mrcc/cli/mrcc --yql -s //home/crypta/team/mskorokhod/cc_graph -d //home/crypta/team/mskorokhod/cc_graph_res -u c1 -v c2
    [INFO] 2018-08-21 12:23:57,355 :: Starting mrcc
    [INFO] 2018-08-21 12:33:30,144 :: Starting iteration 1
    [INFO] 2018-08-21 13:12:51,812 :: Iteration 1 complete. Large star changes: 150546932. Small star changes: 150554568
    [INFO] 2018-08-21 13:12:51,814 :: Starting iteration 2
    [INFO] 2018-08-21 13:42:29,300 :: Iteration 2 complete. Large star changes: 119875723. Small star changes: 109298451
    [INFO] 2018-08-21 13:42:29,300 :: Starting iteration 3
    [INFO] 2018-08-21 14:13:53,023 :: Iteration 3 complete. Large star changes: 106781022. Small star changes: 85895687
    [INFO] 2018-08-21 14:13:53,024 :: Starting iteration 4
    [INFO] 2018-08-21 14:49:07,092 :: Iteration 4 complete. Large star changes: 40706950. Small star changes: 71060883
    [INFO] 2018-08-21 14:49:07,093 :: Starting iteration 5
    [INFO] 2018-08-21 15:16:54,551 :: Iteration 5 complete. Large star changes: 1464778. Small star changes: 9717
    [INFO] 2018-08-21 15:16:54,552 :: Starting iteration 6
    [INFO] 2018-08-21 15:43:35,064 :: Iteration 6 complete. Large star changes: 4985. Small star changes: 11
    [INFO] 2018-08-21 15:43:35,065 :: Starting iteration 7
    [INFO] 2018-08-21 16:12:05,154 :: Iteration 7 complete. Large star changes: 3. Small star changes: 0
    [INFO] 2018-08-21 16:12:05,155 :: Starting iteration 8
    [INFO] 2018-08-21 16:39:15,733 :: Converged
    [INFO] 2018-08-21 16:39:15,733 :: Finishing mrcc
    ```
