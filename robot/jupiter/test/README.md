# Важно!

Пожалуйста, собирайте и запускайте любой из тестов с флагом `-r`.

# Как собрать тест быстро

```console
cd <test_directory>
ya make -r -DDEBUGINFO_LINES_ONLY --dist --add-protobuf-result -E --add-result='' --force-build-depends -k  # запускает сборку на dist-build и выкачивает результаты
```

После такой сборки запускать нужно так:

```console
ya make -r -DDEBUGINFO_LINES_ONLY -tA --add-protobuf-result --test-stderr  # запускает тест (важно, что с теми же флагами, что и при сборке)
```
