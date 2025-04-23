Бекенд для конкурса "Народный путеводитель"
=====

[Wiki](https://wiki.yandex-team.ru/travel/folk-guide-contest/)

### Запуск на локали
```bash
ya make
./cmd/api/api
```


### тест HTTP
```bash
curl "http://localhost:9000/new-story"
```

### Заливка файлов

SB ресурс с собранным tusd под linux [здесь](https://sandbox.yandex-team.ru/resource/1631383188/view).
Про tusd читать [тут](https://github.com/tus/tusd)


### Разработка в GOLAND
Может появиться проблема при компиляции `tvmauth` или `cgosem`.
Поможет добавить `GO111MODULE=off` и `CGO_ENABLED=0` в конфигурацию запуска.
