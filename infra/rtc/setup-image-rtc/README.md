# RTC host setup images
A special version of RND setup image having all bloatware stripped.

## Images storage
Images stored in S3-MDS. Bucket `setup-rtc-images`. To be able to upload the image you should obtain AAA-related staff as described at https://wiki.yandex-team.ru/mds/s3-api/authorization/.

Yo'll need access to service `Dist(id 808)`, bucket `setup-rtc-images`.

After obtaining access keys set up s3cmd as usual: `s3cmd --configure`.


## Images distribution
Images are distributed using dist_proxy service (a.k.a dist.yandex.ru).

    # custom rtc setup image
    location /images/rtc {
      location ~ /images/rtc/(.*)$ {
          access_log /logs/current-setup-rtc.access.log defaultformat;
          proxy_set_header Host s3.mds.yandex.net;
          proxy_pass      http://[2a02:6b8:0:3400::3:147]/setup-rtc-images/$1;
          proxy_cache             Archive;
          proxy_ignore_headers Expires Cache-Control;
          proxy_cache_use_stale error timeout invalid_header http_500 http_502 http_503 http_504;
          proxy_cache_valid 24h;
          proxy_connect_timeout   5s;
          proxy_cache_lock        on;
          proxy_cache_lock_timeout 120s;
          include nginx_trapdoor.conf;
      }
    }

URL construction rules:

    # dist-url to s3-url
    http://dist.yandex.ru/images/rtc/<path> -> s3://setup-rtc-images/<path>
    # dist-url to mds-proxy url
    http://dist.yandex.ru/images/rtc/<path> -> http://s3.mds.yandex.net/setup-rtc-images/<path>

## Building images
Preferred way to build images is to allocate temporary QYP VM with desired ubuntu version and install `debootstrap` there.

    sudo apt-get install debootstrap

Checkout image tool

    svn cat svn+ssh://arcadia.yandex.ru/arc/trunk/arcadia/infra/rtc/setup-image-rtc/rtc-image-tool.sh > rtc-image-tool.sh

Build the image

    sudo bash rtc-image-tool.sh

Upload the image

    sudo bash rtc-image-tool.sh --upload ubuntu-16.04.tar.bz2
