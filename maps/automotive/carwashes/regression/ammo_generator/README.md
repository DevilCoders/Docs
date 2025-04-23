## Generate

```
ya make && ./ammo_generator
```

## Upload

```
aws --endpoint-url=http://s3.mds.yandex.net \
    --profile maps_stress \
    s3 cp maps-auto-navi-carwashes-ammo \
    s3://maps-load-ammo/maps-auto-navi-carwashes-ammo
```
