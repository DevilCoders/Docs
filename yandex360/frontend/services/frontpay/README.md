# Яндекс.Оплата

## Быстрый старт
> ⚠️ Для разработки необходим [yav cli](https://vault-api.passport.yandex.net/docs/#cli).

```shell
npm ci && npm run dev
```

## Публикация версии

```shell
make publish
```

После сборки на Стартреке автоматически будет создан тикет с новой версией.
Чтобы выкатить патч к уже существующей версии, необходимо установить переменную `TICKET` с номером родительского тикета.
```shell
TICKET=FRONTPAY-000 make publish
```

## Документация

- [Внещнее API](/docs/api.md)
- [Разработка тестов на Hermione](/docs/hermione.md)
- [Конфигурация и переменные окружения](/docs/configs.md)

## Полезные ссылки

- [Swagger (Доки по API)](http://payments-test.mail.yandex.net/api/docs/)
- [Шаблоны писем](https://github.yandex-team.ru/inazarov-mi/frontpay-mail-templates)
- [Qloud (Прод)](https://platform.yandex-team.ru/projects/mail/payments-front/production)
- [Qloud (Тест)](https://platform.yandex-team.ru/projects/mail/payments-front/testing)
- [Qloud (QA)](https://platform.yandex-team.ru/projects/mail/payments-qa)
- [Логи (Контейнер)](https://yql.yandex-team.ru/Operations/W6jkKDo4Qf1Tq53Ga7TL3nnEyIGsRapBmLDSbYjWUKw=)
- [Логи (Балансер)](https://yql.yandex-team.ru/Operations/W6jnoTo4Qf1Tq57Y4AlRW5A_uasbjsyXyk-UzfRCOtg=)
- [Голован](https://yasm.yandex-team.ru/panel/inazarov-mi.frontpay/)

