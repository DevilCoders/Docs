# Patcher tool

Takes edges table from road graph yt tables and patches the data in it using a foreign table that matches some persistent_ids with a new data.

### Usage example
```
./patcher -c hahn -i <path_to_road_graph_directory> -d <path_to_table_with_diff> -f <field1> -f <field2> -o <path_to_resulting_table> -v
```
