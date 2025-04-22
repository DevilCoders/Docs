## MoatPagesJob

### Продукт/подсистема

Интеграция с измерителем Moat.


### Роль в работе продукта/подсистемы

Выгружает список PageId и доменов на которых были показы за последние сутки


### Датафлоу

- Запускает YQL запрос, который выгружает данные из chevent лога БК, ищет в них показы по директовым таблицам `banner_measurers`, `camp_measurers`. В последних должны быть bid/cid кампании с типом измерителя `moat`.
- Формирует `.csv`  файл


### Способы наблюдения за текущим состоянием
- [Juggler-проверка](https://juggler.yandex-team.ru/check_details/?host=checks_auto.direct.yandex.ru&service=jobs.MoatPagesJob.working.production&query=&last=1DAY)
- [Логи](https://direct.yandex.ru/logviewer/short/1_3BK7vz4GyZcq)


### Какая функциональность пострадает от отказа джобы

- Партнеры (Moat) перестанут получать свежие данные по площадкам



### Как пользователи (или команда) заметят проблему и через какое время

- На FTP-сервере перестанут появляться выгрузки (Реквизиты https://yav.yandex-team.ru/secret/sec-01ensx32hmky1p5yszrwvxjh80/explore/versions)


### Контакты разработчиков и менеджеров

Разработчики: [login](https://staff.yandex-team.ru/oxid) <br/>
Менеджеры: [login](https://staff.yandex-team.ru/andreypav)


### Желательное время исправления в случае поломки

1-2 дня


### Способы регулирования работы джобы

- Изменения в адресе ftp-сервера или пути директории
- Изменения yql





