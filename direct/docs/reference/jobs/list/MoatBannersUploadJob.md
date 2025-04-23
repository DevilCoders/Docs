## MoatBannersUploadJob

### Продукт/подсистема

Интеграция с измерителем Moat.


### Роль в работе продукта/подсистемы

Отправляет в Moat выгрузку по баннерам с подключенным измерителем moat на их FTP-сервер.


### Датафлоу

- Собираются данные из `banner_measurers`, `banners`, `banners_performance`, `perf_creatives`, `phrases`, `campaigns`, `clients`, `users`
- Формируется `.csv` файл.
- Отправляется на ftp-сервер.


### Способы наблюдения за текущим состоянием

- [Juggler-проверка](https://juggler.yandex-team.ru/check_details/?host=checks_auto.direct.yandex.ru&service=jobs.MoatBannersUploadJob.working.production&query=&last=1DAY)
- [Логи](https://direct.yandex.ru/logviewer/#~(logType~'messages~form~(fields~(~'log_time~'host~'service~'method~'trace_id~'span_id~'prefix~'log_level~'class_name~'message)~conditions~(service~'direct.jobs~method~'moatexport.MoatBannersUploadJob)~limit~100~offset~0~reverseOrder~true~showTraceIdRelated~false))$)


### Какая функциональность пострадает от отказа джобы

- Партнеры (Moat) перестанут получать свежие данные по банерам с измерителем Moat.


### Как пользователи (или команда) заметят проблему и через какое время

- На FTP-сервере перестанут появляться выгрузки (Реквизиты https://yav.yandex-team.ru/secret/sec-01ensx32hmky1p5yszrwvxjh80/explore/versions)
- У пользователей сломается интеграция с Moat.


### Контакты разработчиков и менеджеров

Разработчики: [Саид Аммаев](https://staff.yandex-team.ru/ammsaid), [Алексей Александров](https://staff.yandex-team.ru/hrustyashko)



### Желательное время исправления в случае поломки

1 - 2 дня.


### Способы регулирования работы джобы

- Изменения в адресе ftp-сервера или пути директории


### Известные причины поломок




### Дополнительно: тонкости и подводные камни

- Если вылетит warning с текстом `Unexpected large data size (>5Mb) in shards: <shard>`, то нужно будет разобраться. 5 Мб данных не должен принести проблем, но это выше ожидаемого размера. Если текущий размер данных не ожидаемый, то разобраться откуда так много данных. Если ожидаемый, то можно подвинуть этот порог, однако будет крайне важно убедиться, что нынешний размер не переполнит память при чтении с mysql базы или при формировании .csv файла.
