# Панель продуктовых метрик турбоаппа такси в YASM

Общая конфигурация шаблона панели YASM -
`services/taxi/monitorings/.yasm.main.jinja`

-   [Панель Production окружения](https://yasm.yandex-team.ru/template/panel/turboapp-taxi-metrics/environment=production/)
-   [Панель Testing окружения](https://yasm.yandex-team.ru/template/panel/turboapp-taxi-metrics/environment=testing/)
-   [Панель Development окружения](https://yasm.yandex-team.ru/template/panel/turboapp-taxi-metrics/environment=development/)
-   [Шаблон панели](https://yasm.yandex-team.ru/template/panel/turboapp-taxi-metrics/)

-   Для выбора окружения, нужно подставить environment из саджеста
```bash
environment=<environment>
```

-   Для выбора всех environment'ов сразу -

```bash
environment=all
```
