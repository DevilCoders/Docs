# CCTV PROCESSOR

Processor connects to ССTV cameras. It stores and process frames. 

wiki: https://wiki.yandex-team.ru/users/svetoch/cctv

## Build

```bash
sudo apt install -y libgtest-dev liblapack-dev libblas-dev liblapack-dev libyaml-cpp-dev rapidjson-dev gtk+-3.0 libcurl4-openssl-dev libcurlpp-dev

make build-processor
```

## Build deb

```bash
make deb-processor
```

## Deploy on test server

1. Set "build" host and path to source `processor/tools/test_deploy/inventory.yaml`
2. Add real data to `processor/config/yandex-cctv-processor-config.yaml`
2. CPU
    2. Run `ansible-playbook -i processor/tools/test_deploy/inventory.yaml processor/tools/test_deploy/cpu/deploy_test.yaml`
3. CUDA
    2. Run `ansible-playbook -i processor/tools/test_deploy/inventory.yaml processor/tools/test_deploy/cuda/deploy_test.yaml`


# CCTV MVP

wiki: https://wiki.yandex-team.ru/users/svetoch/cctv/one-month-mvp/

# Prepare
## Ubuntu
Prepare:

`sudo apt install libgtest-dev liblapack-dev libblas-dev liblapack-dev libyaml-cpp-dev rapidjson-dev`

CMake:

```bash
mkdir -p build
cd build
cmake -DCMAKE_BUILD_TYPE=Debug .. [-DWITH_CUDA=OFF]
```

##MacOS
**TODO:**
