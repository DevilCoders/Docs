Process of deleting metrics in PS MegaGraphite
----------------------------------------------

0. Build tools
  ```
$ ./build.sh
```
1. Dump metrics
  ```
$ ./dump.sh ps ps.txt
```
2. Filter metrics which are not updated more than 45 days
  ```
$ ./filter.sh ps.txt ps_to_delete.txt 45
```
3. Compress and upload resulting file to the Sandbox.
4. Notify users about metrics gonna be deleted.

5. Filter out some usefull metrics `from ps_to_delete.txt`
6. Split metric names and metric ids (use correct file as input!)
  ```
$ ./split.sh ps_to_delete.txt ps_to_delete.names ps_to_delete.ids
```
or
5&6. Do split and filter at the same time
  ```
$ ./split_and_filter.sh ps_to_delete.txt.gz "^(cluster|virlab)." "regexp_for_metrics_to_force_delete"
```

7. Delete metrics metadata from Kikimr
  ```
$ ./delete_meta.sh ps ps_to_delete.names
```
8. Restart mega-graphite-storage processes
9. Wait 1-2 days
10. metrics data from Stockpile (SAS)
  ```
$ ./delete_data.sh sas ps_to_delete.ids
```
11. Wait 1-2 days
12. Delete metrics data from Stockpile (VLA)
  ```
$ ./delete_data.sh vla ps_to_delete.ids
```

