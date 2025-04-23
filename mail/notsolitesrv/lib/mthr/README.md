# Библиотека для правил склейки писем в тред
Код перенесен и адаптирован из исходного репозитория [fastsrv](https://github.yandex-team.ru/mail/fastsrv/tree/master/src) по спецификации [delivery-spec/mthr](https://github.yandex-team.ru/mail/delivery-spec/tree/master/apphost/mthr)

## Структура:
* src - реализация алгоритма правил склейки
* ut  - UNIT-тесты

## Сборка:
```bash
ya make mail/notsolitesrv/lib/mthr --checkout
```

## Тестирование:
### UNIT-тесты:
```bash
ya make -t mail/notsolitesrv/lib/mthr --checkout
```
