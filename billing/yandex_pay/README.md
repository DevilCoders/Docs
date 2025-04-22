# yandex_pay

Бэкенд проекта [Yandex.Pay](https://abc.yandex-team.ru/services/yandexpay)

### Разработка

Интерпретатор с зависимостями проекта находится в `$ARCADIA/billing/yandex_pay/python`, собирается через `ya make`.
Данный интерпретатор можно использовать в PyCharm по [этому рецепту](https://i-dyachkov.at.yandex-team.ru/1)

Если нужно работать с protobuf, и хочется чтобы IDE подсвечивало импорты, нужно при сборке добавить параметр `--add-protobuf-result`.

### Тестирование

#### Туннель

Если нужно запустить бэкэнд, и увидеть настоящий ответ с тестинга, то нужно проделать следующее:

1. В QYP есть [машинка](https://qyp.yandex-team.ru/vm/sas/hmnid-yandex-pay) которая привязана к _YANDEXPAY_TEST_NETS_ . Само содержимое тачки тебе не нужно, она используется для туннеля.

2. Нужно socks5 ssh туннель поднять. Это команда `make tunnel`.

3. Создай файл override.conf и положи туда строчку `SOCKS_PROXY = 'socks5://localhost:4444'`.

4. Запускать бэк нужно вот так: `YANDEX_PAY_EXTRA_CONFIG_FILE=./override.conf make l_runserver`.

### TVM
Чтобы добавить запуск tvmtool нужно:
1. Положить в `.tvm.key` [секрет](https://yav.yandex-team.ru/secret/sec-01epw4erh4b5c917gdkrk7v636/explore/versions).
2. В `run_local.sh` прописать `self_tvm_id`.
Между перезапусками нужно самостоятельно удалять `.tvm.json`, если была ошибка запуска tvmtool.

### Развертывание в Ya.Deploy
Шаблоны спек Ya.Deploy храним в каталоге ./deploy

Принято соглашение о развертывании двумя способами:
1. Если спека не меняется, то катим через интерфейс CI в аркануме. В меню CI арканума нужно найти проект Yandex Pay, выбрать сбоку Release. Запустить на нужном коммите.
Сначала собирается и пушится пакет, далее деплой в три окружения последовательно. Деплой на testing автоматический, на sandbox и production с ручным подтверждением.
Документация по CI: https://docs.yandex-team.ru/ci/
1. Если спека меняется, то катим руками. Для того, чтобы катнуться:
   * синхронизируем спеку `make sync-deploy-spec`
   * редактируем шаблон спеки, желательно поправить `description` на что-то понятное
   * запускаем `make yadeploy-(testing|load|sandbox|production)`.

### Обновление геобазы
1. `make geobase`
2. Взять rbtorrent урл и указать в спеке у ресурса с id: GeoBase
