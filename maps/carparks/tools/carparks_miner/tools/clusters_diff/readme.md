This tool checks all clusters from two specified tables
and finds difference between them.
input: yt paths for two clusterized_points tables and yt-directory path for results
output: difference between tables:
    - table with the same clusters
    - table where main clusters change their order
    - table where clusters exist in first table, but not in second
    - table where clusters exist in second table, but not in first
    - table with completly different clusters

Usage example:

```
./versions_comparision --old {path_for_old_clusterized_table} --new {path_for_new_clusterized_table} --destination {path_for_results_directory}
```