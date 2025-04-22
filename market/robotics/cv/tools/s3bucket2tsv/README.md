# S3 Bucket to TSV file

This util allow to collect files from bucket with prefix and generate TSV file for it.
To get access, visit page with [How To Work with S3](https://wiki.yandex-team.ru/roboticsmarket/manuals/s3-manual/)

## Launching example
```bash
./s3bucket2tsv --key-id <your-key-id> --secret-key <your-secret-key> --bucket-name <backet_name> --prefix <prefix-folder> --recursive --with-id --endpoint-url http://s3.mds.yandex.net
```
