# ymaps-proto
YMaps Router and Matrix Router protobuf classes

# Instruction
- ~~update `maps/routing/matrix_router/proto` from the same path in arcadia~~ // v1 matrix router
- update `yandex/maps/proto` from `arcadia/maps/doc/proto/yandex/maps/proto` in arcadia
- compile using compile.sh
- install with pip
- push compiled proto files to this repository

## Location of proto classes for each router:
- Matrix Router v2:  `yandex/maps/proto/driving_matrix`
- Driving router: `yandex/maps/proto/driving`
- Transit router: `yandex/maps/proto/masstransit`
- (**Will be deprecated soon**) Matrix Router v1: `maps/routing/matrix_router/proto`

# Requirements
Requires python `protobuf` compiler: `protoc --version` ≤ libprotoc 3.4.0  
The older versions generate classes for python3  
protoc installation: https://askubuntu.com/questions/1072683/how-can-i-install-protoc-on-ubuntu-16-04

# Compile Classes
`protoc -I $src_pkg --python_out=$dst_pkg <file.proto>`
 
Compile all classes in in repository using  `./compile.sh`

# Install lib with pip
## Install from VCS
First, check that all directories you need to install contain `__init__.py` file. Or create files using
`cd yandex/maps/proto ; find ./ -mindepth 1 -maxdepth 2 -type d | while read d; do echo $d; cp __init__.py $d/ ; done`

Now install:
`pip install -U -i https://pypi.yandex-team.ru/simple svn+ssh://arcadia.yandex.ru/arc/trunk/arcadia/maps/b2bgeo/analytics/ymaps-proto`

## Install from pip
`pip install -U -i https://pypi.yandex-team.ru/simple ymaps-proto`

# Publish to pip
How to upload a new package version:
- https://wiki.yandex-team.ru/pypi/#zagruzkapaketov

Take pypi_access_key and pypi_secret_key from here: https://yav.yandex-team.ru/secret/sec-01ddnqy4dyqvjxcgt8vp83v7jc/explore/version/ver-01g0y8aqmpdsycvbmfx91vx5jq
