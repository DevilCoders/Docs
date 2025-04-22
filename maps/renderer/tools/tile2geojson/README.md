Outputs a tile as line delimited stream of GeoJSON layers.

Example.
Export for QGIS.
```sh
wget -qO - "http://vec01.maps.yandex.ru/nav2?l=vmap2&x=38295&y=19117&z=16&zmin=15&zmax=19&lang=ru_RU" \
       | ./tile2geojson -t '38295,19117,16' -z 18 \
       | tac \
       | split -l 1 --additional-suffix=.geojson - ~/tmp/layer
```

