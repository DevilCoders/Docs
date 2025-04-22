### Типичный цикл работы

`cd direct/solo`

Обновить код  
`ya make -j0 --checkout`

Поредактировать что хочешь

Собрать проект  
`ya make`

Прогнать тесты  
`ya make -rA`

Посмотреть, какие изменения оно собиратеся сделать в Соломоне/Juggler/etc  
`./creator/creator --oauth`

или  
`SOLOMON_TOKEN=<...> JUGGLER_TOKEN=<...> NANNY_TOKEN=<...> ./creator/creator`

Применить правки  
`./creator/creator --oauth --apply-changes`
(в будущем это не надо делать из своей рабочей копии, будет автоприменение из репозитория)

Закоммитить


### Где посмотреть результаты работы

Дашборды в Соломоне можно искать через страницу "Все дашборды Директа" <https://solomon.yandex-team.ru/?project=direct&dashboard=direct-all-dashboards>


### Соглашения

- Дашбордам в конце имени давать суффикс `(Solo)`. Пример: `L7 Total Dashboard (Solo)`
- графикам, алертам — тоже давать суффикс (`#solo` или `(Solo)`)


### TODO

1) вынести секреты робота для доступа к соломону
2) поддержать деплой ci
