# Админка Яндекс.Оплаты

## Быстрый старт
> ⚠️ Перед запуском необходимо [подключить tvm ключ](#как-подключить-tvm-ключ) и [добавить конфиг приложение](#как-добавить-конфиг-приложение).

```shell
npm install
npm run start:dev
```

### Как подключить tvm ключ?

Создать файл `.tvm.key` с tvm ключом в корне проекта.

Где взять ключ?
1. Ключ для dev [тут](https://yav.yandex-team.ru/secret/sec-01epc4czegxkpdt4v0dw1gpmek/explore/version/ver-01fctczyrk42v73tgs15er18bq)
2. Ключ для тестинга можно найти [здесь](https://abc.yandex-team.ru/services/pay/resources/?show-resource=4160466)
3. Узнать у @mishk0 или @inazarov-mi

### Как добавить конфиг приложение?

Скопировать dev конфиг:
```shell
cp ./.env.development.example ./.env.development
```

## Публикация версии
```shell
make publish
```

После сборки на Стартреке автоматически будет создан тикет с новой версией.
Чтобы выкаить патч к уже существующей версии, необходимо добавить установить переменную `TICKET` с номером родительского тикета.
```shell
TICKET=FRONTPAY-000 make publish
```

## Полезные ссылки

- [Swagger (Доки по API)](http://payments-unstable.mail.yandex.net/admin/api/docs)
- [Qloud (Прод)](https://platform.yandex-team.ru/projects/mail/payments-front/admin-production)
- [Qloud (Тест)](https://platform.yandex-team.ru/projects/mail/payments-front/admin-testing)
- [Qloud (QA)](https://platform.yandex-team.ru/projects/mail/payments-qa)
- [Error counter](https://error.yandex-team.ru/projects/zigzag)
- [Голован](https://yasm.yandex-team.ru/panel/inazarov-mi.zigzag)
