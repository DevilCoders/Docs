# Library for calculating sign position accuracy.

## Contains:
* datasets with mrc gps tracks, sensors and photos
* lib for loading datasets, calculating signs position accuracy, visualize signs positions
* signs position algorithm that uses several photos of one sign

## How to run(example):
```
cd datasets
ya make
cd ../algorithm_several_photos
ya make
./mrc-signs-position --out-geojson output1.geojson --dataset ../datasets/maps-mrc-signs-positioning-dataset/7a618fc0808d3984dc44b8baead2c1cc-1546158440000000000
```

### or
```
./mrc-signs-position --out-geojson output1.geojson --assignment-id=10760 --source-id='4d50e2816a2c5e39dc206b9e045299d4'
```