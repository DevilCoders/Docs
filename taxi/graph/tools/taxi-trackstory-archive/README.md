Example usage:

AWS_ACCESS_KEY_ID=<MDS_ACCESS_KEY> \
AWS_SECRET_ACCESS_KEY=<MDS_SECRET_KEY> \
./taxi-trackstory-archive \
        --yt-proxy hahn \
        --source-table="//home/taxi/home/vaninvv/tracker1h" \
        --destination-table="//home/taxi/home/vaninvv/removeme" \
        --mds-bucket=taxi-camera-testing \
        --mds-host=s3.mdst.yandex.net \
        --mds-prefix=testdata
