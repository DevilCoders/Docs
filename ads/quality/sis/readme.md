## Arcadia build

Для сборки необходимо добавить флаги

```-DCUDA_VERSION=11.4 --host-platform-flag=CUDA_VERSION=11.4```

Для генерации проекта CLion

```ya ide clion --make-args=-DCUDA_VERSION=11.4 --make-args=--host-platform-flag=CUDA_VERSION=11.4```

Запуск тестов

```ya make -Art -DCUDA_VERSION=11.4 --host-platform-flag=CUDA_VERSION=11.4```

Запуск тестов на YT

```YT_TOKEN_PATH=~/.yt/token ya make -Art --run-tagged-tests-on-yt -DCUDA_VERSION=11.4 --host-platform-flag=CUDA_VERSION=11.4```

## CMake build

В sis/contrib надо добавить:
  - [cutlass 2.9](https://github.com/NVIDIA/cutlass)
  - [TensorRT 8](https://developer.nvidia.com/nvidia-tensorrt-download)

Запуск тестов ```tests/run_parallel.py```