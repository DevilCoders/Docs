# Список экспериментальных флагов

Директория с флагами экспериментов. Один флаг — один файл.

**пример:**

Имя флага: `disable_promo_logo`

Имя файла: `disable_promo_logo.json`

Содержимое файла:

```json
{
  "date": "19.11.2015",
  "description": "SERP-32658: Праздничный логотип на серпе",
  "manager": "vtenity",
  "dataDependent": false,
  "system": true,
  "values": {
      "Включить функциональность": 1
  },
  "service": [
      "web",
      "images",
      "video"
  ],
  "platforms": [
    "desktop",
    "touch-pad",
    "touch-phone"
  ],
  "validation_type": "json"
}
```

Поле `manual` указывает на то, что флаг используется не только в репозитории web4, но и в других репозиториях. По умолчанию все флаги считаются автоматическими, поэтому перед тем, как добавить флаг, необходимо проверить [хранилище][ab_flag_storage] на наличие флагов с таким же именем, а также проекты, подключенные к [системе автоматического обновления флагов][infra_expflags_auto].

> :warning: Обязательно прочтите про [процесс добавления флагов в проект][infra_add_new_flag].

Поле `dataDependent` показывает, является ли функциональность под флагом зависимой от данных, которые так же включаются флагом. Поле может отсутствовать.

Поле `system` показывает, что флаг системный и не участвует в экспериментах, а используется как системная настройка. Поле может отсутствовать.

Поле `service` содержит список сервисов, в которых будет раскатан флаг. По умолчанию, если поле не заполнено, будет использоваться три сервиса: web, images, video.

Отнеситесь серьезно к заполнению поля `validation_type`. Ошибка может привести к инциденту [SEARCHPRODINCIDENTS-3213](https://st.yandex-team.ru/SEARCHPRODINCIDENTS-3213#1519643483000)

**Возможные значения**

| validation_type | пример       |
| ----------------|:-------------|
| json            | `"json_attr": "some json value"`
| str             | `"string_attr": "строка"`
| int             | `"int_attr": 42`
| float           | `"float_attr": 3.14`
| bool            | `"boolean_attr": true`
| 01              | `"01_attr": 1`
| list_of_str     | `"list_of_str_attr": ["value1", "value2", "value3"]`

## Тулза для создания новых флагов

Файлы можно создавать через консольную утилиту, где в интерактивном режиме можно задать все необходимые поля. Запускается из корня проекта:

```bash
npm run flag:create
```

[ab_flag_storage]: ab.yandex-team.ru/flag_storage
[infra_add_new_flag]: https://wiki.yandex-team.ru/search-interfaces/infra/infraspeed/docs/expflags/expflags-regulations/#processdobavlenijaflagavproekt
[infra_expflags_auto]: https://wiki.yandex-team.ru/search-interfaces/infra/infraspeed/docs/expflags/expflags-regulations/#kakixproektovjetokasaetsja
