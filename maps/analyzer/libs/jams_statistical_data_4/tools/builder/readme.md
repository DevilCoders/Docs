Use this binary to convert stat table to mms. Example:
```bash
yt read //path/to/table --format yson | ./builder --edges-count `yt get //path/to/table/@row_count` --version "test-"`date -I` --output stats.mms
```
