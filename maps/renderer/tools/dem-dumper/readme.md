## Engine documentation
<https://wiki.yandex-team.ru/users/goodkov/dem>

## Usage
```
ya make -r
cd scripts
```

### Download DEM sources:
```
./down.all.sh
```
Downloads both ASTER & NASADEM datasets, file resume supported.

ASTER (for zooms 3-11): required ~= 30GB space, Yandex MDS resources, < 1 hour.

NASADEM (for zooms 12-14): required ~= 130GB, **external resources**, download time ~= 15 hours.

Results in `./src3`(ASTER) and  `./src1`(NASADEM) folders.

### Process:
```
./dump.all.sh
```
Requirements: 25GB disk space, 100GB RAM.

Full dump takes ~= 6 hours with 48 cores.

### Pack renderer datasource:
```
./pack.sh 			
```
+Yet another 25GB of disk space.

### Upload renderer datasource:
```
./upload.sh
```
When the task is completed (~1 hour), do not forget to release it:

<https://sandbox.yandex-team.ru/resources?type=MAPS_RENDERER_DEM_SOURCE>

After resource release, you can expect terrain data to be updated in basemap after next basemap build (typically 12 noon next day). Cartograph use terrain data from basemap build too.