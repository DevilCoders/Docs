### HOWTO BUILD

```
mkdir nginx
cd nginx/
git clone git@github.yandex-team.ru:morda/nginx.git .
git submodule update --init
sudo apt-get build-dep nginx
sudo dpkg-buildpackage -b
```

### HOWTO INSTALL
```
sudo apt-get install libjson-c2 libticket-parser
sudo dpkg -i nginx_1.8.1-1.yandex.20_amd64.deb
```
### HOWTO upload
```
dch
debsign XXX.changes
dupload XXX.changed
```

### 2017-03-15
patched with https://github.com/nginx/nginx/commit/50ff8b3c3a3eba0984ce55c63ab8ac07dcb65265

### 2017-05-26
patched with http://hg.nginx.org/nginx/rev/062c189fee20 ssl

patched with http://hg.nginx.org/nginx/rev/97c99bb43737 worker_shutdown_timeout (reverted)

### поддержка brotli_static
https://github.com/google/ngx_brotli
