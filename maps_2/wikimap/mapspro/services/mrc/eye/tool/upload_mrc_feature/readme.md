# upload-mrc-feature

## Overview
Upload mrc features from db to YT table in yson format.

```
# store feature ids in file (splited with \n)
upload-mrc-feature \
    --secret-version "ver-12345" \
    --mrc-config config.xml \
    --feature-ids feature_ids.txt \
    --yt-table //tmp/example

# read feature ids from stdin
psql -At -c "SELECT feature_id FROM signals.feature WHERE ..." | upload-mrc-feature \
    --secret-version "ver-12345" \
    --mrc-config config.xml \
    --yt-table //tmp/example
```