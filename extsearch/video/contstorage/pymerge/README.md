

basis:

- process portions, export 5min windowed streams
- split windowed to 2 tables: url->hash, hash->content
- shard content
- merge windowed streams to delta
- remove duplicates from delta, filter existance content
- merge delta with state



