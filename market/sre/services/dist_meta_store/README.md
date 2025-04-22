# Dist Meta Store
> A MVP of service for storing meta information of dists

## Usage example

```
> cmd/dist-meta-store-server/dist-meta-store-server -port 8079 -grpc-port 8080
2019/05/16 15:33:38 connection to database has been establish and ping succeed
2019/05/16 15:33:38 http listener to localhost:8079 has been created
2019/05/16 15:33:38 grpc listener to localhost:8080 has been created
...
>
```

```
> curl localhost:8079/ping
0;OK
> cmd/dist-meta-store-client/dist-meta-store-client -action add -dist search-part-2 -generation 20190512_2226 -rbtorrent rbtorrent:693640cc7f78d96148f0667547715d0a19d04847 -dc sas
2019/05/16 15:33:58 dist has been added
> cmd/dist-meta-store-client/dist-meta-store-client -action find -dist search-part-2 -generation 20190512_2226 -dc sas
2019/05/16 15:34:05 dist:"search-part-2" dc:"sas" generation:"20190512_2226" rbtorrent:"rbtorrent:693640cc7f78d96148f0667547715d0a19d04847" 
>
```

## MVP
Nanny services https://nanny.yandex-team.ru/ui/#/services/dashboards/catalog/market_dist_meta_store/  
LB https://racktables.yandex-team.ru/index.php?page=ipvs&vs_id=7458  
Endpoint dist-meta-store.tst.vs.market.yandex.net:8080  
PGaaS https://yc.yandex-team.ru/folders/fooeehq0fj9a6o9c6fe1/managed-postgresql/cluster/mdbf28idkl9129r3ps0s  
YAV https://yav.yandex-team.ru/secret/sec-01db5gmnk4m88njyrvnke8495p/explore/versions  

## TODO
1. Add monitoring, handler `/monitoring`
2. Add support for using several servers for postgresql
3. Add metrics, handler `/unistat` for YASM 

## Links

https://st.yandex-team.ru/CSADMIN-28474
https://st.yandex-team.ru/MARKETTECH-655
