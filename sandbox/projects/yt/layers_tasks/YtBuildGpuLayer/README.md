## Infiniband packaging

Current package (2020.12.10): https://sandbox.yandex-team.ru/resource/1876666601/view

### How to build it

1.  Put into /etc/apt/sources.list.d/search-upstream-m1x5.list
```
deb http://search-upstream-mlx5-1-xenial.dist.yandex.ru/search-upstream-mlx5-1-xenial unstable/all/
deb http://search-upstream-mlx5-1-xenial.dist.yandex.ru/search-upstream-mlx5-1-xenial unstable/amd64/
```

2. Download following packages: (apt-get download ibverbs-providers=51mlnx1-1.51258)
```
ibverbs-providers_51mlnx1-1.51258_amd64.deb
libibverbs1_51mlnx1-1.51258_amd64.deb
libibverbs-dev_51mlnx1-1.51258_amd64.deb
libnl-route-3-200_3.2.29-0ubuntu3_amd64.deb
librdmacm1_51mlnx1-1.51258_amd64.deb
```

3. Extract this packages by ```dpkg -x my_pkg.deb output_dir/```

4. Cleanup:

```
rm -rf output_dir/usr/share
rm -rf output_dir/usr/include
find output_dir/ -name "*.a" | xargs rm
```


### How to test it

* Run operation: ```yt map 'sleep 10000;' --spec '{pool = research_gpu; pool_trees = [gpu_tesla_a100]; mapper = {gpu_limit = 1; layer_paths = ["//porto_layers/cached_in_tmpfs/bionic_base"];}}' --local-file /usr/bin/ib_write_bw --local-file /usr/bin/ibv_devinfo ... (some src/dst/format params)```
* Ssh inside one job and run ```./ib_write_bw -d mlx5_0 --ipv6-addr```
* Ssh inside another job on the same host and run ```./ib_write_bw -d mlx5_0 --ipv6-addr localhost```
* Some information about sent bytes should appear.
