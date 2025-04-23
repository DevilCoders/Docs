# Sync
Позволяет обновить локальную копию конфигурации проектов:
```
$ ./cli sync
```
Файлы нужно коммитить вручную.

# Groupper
## Goals
Разобраться в маштабе разных конфигураций (по полям) в проекта.

## How to
Проще всего понять на примере. Мы хотим узнать на каком количестве проектов с тегами `rtc`, `yp` есть разница между `automation_plot_id`

```
$ ./cli groupper -t rtc,yp automation_plot_id
automation_plot_id:
  unique values: 1
  variants:
  - ids: yp-iss-iva, yp-iss-man, yp-iss-man-dev, yp-iss-man-yt-hume, yp-iss-man-yt-hume-lvm,
      yp-iss-myt, yp-iss-new, yp-iss-prestable, yp-iss-prestable-base-search, yp-iss-sas,
      yp-iss-sas-base-search, yp-iss-sas-dev, yp-iss-sas-yt-hahn, yp-iss-vla, yp-iss-vla-dev,
      yp-iss-xdc, yp-iva, yp-man, yp-man-pre, yp-msk, yp-sas, yp-sas-test, yp-testing,
      yp-testing-2, yp-vla, yp-xdc
    value: rtc
```
Опционально можно передать путь к каталогу с конфигами через `--configs-dir`.
Последующие аргументы это теги и поле которое интересует.
Теги можно не только включать, но и исключать:
```
$ ./cli groupper -t rtc,yp,-yt,-rtc.scheduler-none cms_api_version
cms_api_version:
  unique values: 2
  variants:
  - ids: yp-iss-iva, yp-iss-iva-dev, yp-iss-man, yp-iss-man-dev, yp-iss-myt, yp-iss-myt-dev,
      yp-iss-prestable, yp-iss-prestable-base-search, yp-iss-prestable-yard, yp-iss-sas,
      yp-iss-sas-base-search, yp-iss-sas-dev, yp-iss-vla, yp-iss-vla-dev, yp-iss-xdc,
      yp-testing, yp-testing-lvm, yp-testing-mtn
    value: v1.0
  - ids: yp-testing-2
    value: null
```

А еще можно искать внутри dict'a
```
$ ./cli groupper -t rtc,yp -f notifications.recipients.error
notifications.recipients.error:
  unique values: 9
  variants:
  - ids: yp-iss-sas-dev, yp-iss-vla-dev
    value:
    - basic@yandex-team.ru
    - slonnn@yandex-team.ru
    - vminkov@yandex-team.ru
    - amich@yandex-team.ru
    - frolstas@yandex-team.ru
  - ids: yp-iss-iva, yp-iss-man, yp-iss-myt, yp-iss-new, yp-iss-xdc
    value:
    - basic@yandex-team.ru
    - vminkov@yandex-team.ru
    - slonnn@yandex-team.ru
  - ids: yp-man-pre, yp-msk
    value:
    - yp-monitoring@yandex-team.ru
  - ids: yp-testing, yp-testing-2
    value:
    - basic@yandex-team.ru
  - ids: yp-iss-man-dev
    value:
    - basic@yandex-team.ru
    - vminkov@yandex-team.ru
    - slonnn@yandex-team.ru
    - frolstas@yandex-team.ru
  - ids: yp-iss-vla, yp-iva, yp-man, yp-sas-test, yp-vla, yp-xdc
    value: []
  - ids: yp-sas
    value:
    - stunder@yandex-team.ru
    - yp-monitoring@yandex-team.ru
  - ids: yp-iss-man-yt-hume, yp-iss-man-yt-hume-lvm, yp-iss-sas-yt-hahn
    value:
    - wall-e-search-notifications@yandex-team.ru
  - ids: yp-iss-prestable, yp-iss-prestable-base-search, yp-iss-sas, yp-iss-sas-base-search
    value:
    - basic@yandex-team.ru
    - slonnn@yandex-team.ru
    - vminkov@yandex-team.ru
    - amich@yandex-team.ru
```
