## Panther workers

### Some init commands

#### FS init

```
./yt_dynamic_tables create-tables --yt-proxy hahn --yt-dir //home/saas2/test/panther/worker --ssd --disable-replicas --content-tablet-count 10

./yt_dynamic_tables init-shards --yt-proxy hahn --yt-dir //home/saas2/test/panther/worker --schema ~/arcadia/search/plutonium/workers/panther/configs/l2/panther.tablet_mapping.schema.pb.txt --state-id-generator iso8601us
```

#### Queue init
```
YT_PROXY=hahn ./big_rt_cli queue create //home/saas2/test/panther/out_queue --shards 10 --medium ssd_blobs --max-ttl 30m
yt set '//home/saas2/test/panther/out_queue/@allowed_proto_types' '["NPlutonium::NWorkers::NPanther::TBannerProfileWithGuts"]' --proxy hahn
yt set '//home/saas2/test/panther/out_queue/@queue_format_flags' '["enable_frame_unpacker"]' --proxy hahn
YT_PROXY=hahn ./big_rt_cli consumer create //home/saas2/test/panther/out_queue test_consumer --ignore-in-trimming 1
```
