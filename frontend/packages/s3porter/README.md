# s3porter

Утилита для деплоя файлов в S3.
Написана под Node.js.
Решает следующие проблемы:

- aws-cli не умеет понимать mime-type файлов сжатых brotli
- для js-файлов используется mime-type `text/javascript` для поддержки в старых браузерах
- есть возможность проверять, что все файлы сжаты и досжимать несжатые

## Как установить:

```bash
npm i -D @yandex-int/s3porter --registry=https://npm.yandex-team.ru
# или
yarn add -D @yandex-int/s3porter --registry=https://npm.yandex-team.ru
```

## Как пользоваться:

cli:

```bash
ℹ️  Usage: cli.js <command>
ℹ️  Usage: cli.js [options] source_directory_or_s3_path destination_s3_path

Commands:
  cli.js deploy  deploys files from local directory or 3s bucket with prefix to
                 s3 bucket with prefix                                 [default]
  cli.js remove  removes all objects from bucket with prefix

Options:
  -h, --help            Show help                                      [boolean]
  --version, -v         version                                        [boolean]
  -e, --endpoint        target endpoint   [default: "https://s3.mds.yandex.net"]
  --validate            validate that all files are compressed
                                                      [boolean] [default: false]
  -c, --compress        compress plain files          [boolean] [default: false]
  --compressionOptions  compression options json config file
  --cache-control       set Cache-Control header of uploaded file (not supported
                        on internal S3)                    [default: "no-cache"]
  --concurrency         amount of simultaneous uploads          [default: "200"]
  --access-key-id       amazon access key id      [default: <AWS_ACCESS_KEY_ID>]
  --secret-access-key   amazon secret access key
                                              [default: <AWS_SECRET_ACCESS_KEY>]

Examples:
  s3porter ./src/ s3://bct/dir              deploy files from local directory
                                            ./src/ to s3 bucket 'bct' with
                                            prefix 'dir/'
  s3porter s3://src_bct/src_dir             deploy files from s3 bucket
  s3://dst_bct/dst_dir                      'src_bct' with prefix 'src_dir/' to
                                            s3 bucket 'dst_bct' with prefix
                                            'dst_dir/'
  s3porter remove s3://bct/dir              removes all objects from s3 bucket
                                            'bct' with prefix 'dir/'
```

js:

```javascript
const s3porter = require("s3porter");
// fs -> s3
s3porter(
  {
    from: "/path/to/upload",
    to: "s3://target-bucket/target-path",
  },
  err => {},
);

// s3 -> s3
s3porter(
  {
    from: "s3://source-bucket/source-path",
    to: "s3://target-bucket/target-path",
  },
  err => {},
);

// s3 -> fs
throw new Error("Not implemented");

// removing
s3porter.removeObjectsByS3Path(
  {
    s3Path: "s3://bucket/prefix-to-removing",
  },
  err => {},
);
```
