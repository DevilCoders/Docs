This tools is created to easily download/replace b2bgeo files on s3.

# Description

Initially used to replace data for https://b2b-geo.slack.com/archives/C1WPWN960/p1619773225110500.

There are 2 modes:
```
$ ./s3_tool download --help
Usage: ./s3_tool download [OPTIONS] [ARG]...

Required parameters:
  {-u|--uuid} Task UUID

Optional parameters:
  {-V|--svnrevision}    print svn version
  {-?|--help}           print usage
  {-t|--type} Either request or response. default: "Request"
```

```
$ ./s3_tool replace --help
Usage: ./s3_tool replace [OPTIONS] [ARG]...

Required parameters:
  {-u|--uuid} Task UUID
  {-f|--file} File with data to replace s3 object

Optional parameters:
  {-V|--svnrevision}    print svn version
  {-?|--help}           print usage
  {-t|--type} Either Request or Response. default: "Request"
```

# Requirements

You need to have access to secret https://yav.yandex-team.ru/secret/sec-01ddnqnbh2mtx5mmw5svht0vv6 to be able to set correct environment variables for run:
```
# testing:
env YC_S3_SECRET_KEY=$(ya vault get version sec-01ddnqnbh2mtx5mmw5svht0vv6 -o AccessSecretKey) YC_S3_ACCESS_KEY=$(ya vault get version sec-01ddnqnbh2mtx5mmw5svht0vv6 -o AccessKeyId) YC_S3_SERVER=s3.mds.yandex.net YC_S3_BUCKET=b2bgeo-dev YC_S3_PREFIX=YC ./s3_tool

# prod:
env YC_S3_SECRET_KEY=$(ya vault get version sec-01ddnqnbh2mtx5mmw5svht0vv6 -o AccessSecretKey) YC_S3_ACCESS_KEY=$(ya vault get version sec-01ddnqnbh2mtx5mmw5svht0vv6 -o AccessKeyId) YC_S3_SERVER=s3.mds.yandex.net YC_S3_BUCKET=b2bgeo YC_S3_PREFIX=YC ./s3_tool
```

# Basic usage for downloading

Downloading request:
```
env YC_S3_SECRET_KEY=$(ya vault get version sec-01ddnqnbh2mtx5mmw5svht0vv6 -o AccessSecretKey) YC_S3_ACCESS_KEY=$(ya vault get version sec-01ddnqnbh2mtx5mmw5svht0vv6 -o AccessKeyId) YC_S3_SERVER=s3.mds.yandex.net YC_S3_BUCKET=b2bgeo-dev YC_S3_PREFIX=YC ./s3_tool download -u 476fb29e-5021c768-53a9111e-b0fb4a20 -t Request
```

Downloading response:
```
env YC_S3_SECRET_KEY=$(ya vault get version sec-01ddnqnbh2mtx5mmw5svht0vv6 -o AccessSecretKey) YC_S3_ACCESS_KEY=$(ya vault get version sec-01ddnqnbh2mtx5mmw5svht0vv6 -o AccessKeyId) YC_S3_SERVER=s3.mds.yandex.net YC_S3_BUCKET=b2bgeo-dev YC_S3_PREFIX=YC ./s3_tool download -u 476fb29e-5021c768-53a9111e-b0fb4a20 -t Response
```

# Advanced usage for replacing (THIS SCENARIO IS VERY RARE)

Replacing request:
```
env YC_S3_SECRET_KEY=$(ya vault get version sec-01ddnqnbh2mtx5mmw5svht0vv6 -o AccessSecretKey) YC_S3_ACCESS_KEY=$(ya vault get version sec-01ddnqnbh2mtx5mmw5svht0vv6 -o AccessKeyId) YC_S3_SERVER=s3.mds.yandex.net YC_S3_BUCKET=b2bgeo-dev YC_S3_PREFIX=YC ./s3_tool replace -u 476fb29e-5021c768-53a9111e-b0fb4a20 -t Request -f request.json
```

Replacing response:
```
env YC_S3_SECRET_KEY=$(ya vault get version sec-01ddnqnbh2mtx5mmw5svht0vv6 -o AccessSecretKey) YC_S3_ACCESS_KEY=$(ya vault get version sec-01ddnqnbh2mtx5mmw5svht0vv6 -o AccessKeyId) YC_S3_SERVER=s3.mds.yandex.net YC_S3_BUCKET=b2bgeo-dev YC_S3_PREFIX=YC ./s3_tool replace -u 476fb29e-5021c768-53a9111e-b0fb4a20 -t Response -f response.json
```
