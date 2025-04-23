## How to build pg 

### Mac
```bash
mkdir pg_resource && cd pg_resource
git clone https://github.com/postgres/postgres.git -b REL_<...>
mkdir build && cd build
../postgres/configure --prefix=(pwd)/../tmp --disable-rpath --with-python --without-readline --with-uuid=e2fs
make world-bin
make install-world-bin
cd .. && mkdir pg && cd pg
cp -r ../tmp/* . && cd .. # по какой-то причине ya upload не грузит файлы timezone, если загружать сразу, без копирования, собранный pg
ya upload --ttl=inf pg/
```

### Linux
```bash
mkdir pg_resource && cd pg_resource
git clone https://github.com/postgres/postgres.git -b REL_<...>
bash arcadia/taxi/cargo/taxi-testsuite-pg/build.sh $(pwd)/postgres $(pwd) # если собирать на виртуалке, то pg будет требовать довольно свежую версию glibc, которой нет на хостах distbuild-а
ya upload --ttl=inf pg/
```
