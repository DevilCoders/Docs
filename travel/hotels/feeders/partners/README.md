### Создаем новый фидер
```
{partner_name}
    ya.make
    __main__.py
    __init__.py
```

`__init__.py` - пустой.

`ya.make`:
```yamake
PY2_PROGRAM()

OWNER(g:travel)

PY_SRCS(
    __main__.py
)

PEERDIR(
    travel/hotels/feeders/lib
)

END()
```

### `__main__.py`
```python
# coding=utf-8
import warnings

import six
from travel.hotels.feeders.lib import base, downloaders, parsers, helpers
from travel.hotels.feeders.lib.model import objects, enums, features_enums

# Для всех ворнингов нужно использовать один из следующих типов (можно добавлять)
from travel.hotels.feeders.lib.model import log_message_types

class FeederName(base.Partner):
    name = "name" # имя фидера (уникальное)

    min_records_count_accepted = None # минимальное количество отелей при котором фид считается успешно построенным
    max_records_added_or_removed_count = None # максимальное удаленное или добавленное количество отелей
    warn_records_count_change = None

    allowed_fields = base.Partner.allowed_fields + [] # скрытые поля - начинающиеся с '_' - которые нужно разрешить в этом фиде
    # Сообщения о непустых скрытых полях будут выводиться при запуске фидера.
    hidden_fields = base.Partner.hidden_fields + [] # общие поля которых нет в этом фиде и которые можно скрыть.
    
    url = ""
    
    # обязательно имплементировать следующие два метода:
    def download_all_feeds(self):
        self.download_and_save(self.url,
            downloader=downloaders.StreamingDownloader(),
            parser=parsers.XmlParser(),
            name='hotels', # Табличка будет сохранена на yt в папке фида https://yt.yandex-team.ru/hahn/navigation?path=//home/travel/prod/feeds/expedia/latest/raw  
            auth=self.auth,
            limit=self.limit)
            
    def map(self, dict_item, info): # dict item - питоновский dict из колонки item в hotels табличке
        hotel = objects.Hotel()
        
        return hotel        
        
    # также может пригодиться:    
    def __init__(self, session, args):
        super(FeederName, self).__init__(session, args)
        self.auth = (args.user, args.password)
        
    @staticmethod
    def configure_arg_parser(parser, proc_env):
        arg_group = parser.add_argument_group(FeederName.name)
        arg_group.add_argument("--user", '-u', default="yandex1")
        arg_group.add_argument("--password", '-p', required=True)
    

if __name__ == '__main__':
    FeederName.main()
```

Поля, которые обязательно заполнить:
```
    hotel.original_id
    hotel.name
    hotel.address 
    hotel.lat 
    hotel.lon
    hotel.country # country code
    hotel.rubric
    
    hotel._partner
``` 
Поля, важные для матчинга:
```
    hotel.url
    hotel.phone
```

### Маппинги - рубрики и признаки.
Для маппинга партнерских значений в наши нужно обратиться к @ritapak
После этого использовать скрипты.
`arcadia/travel/hotels/feeders/scripts/amenities_mapping_codegen`
`arcadia/travel/hotels/feeders/scripts/rubric_mapping_codegen`

для того чтобы воспользоваться скриптами достаточно положить .csv файл от Риты в ./resources
с соответствующим формату названием
и запустить `./rubric_mapping_codegen {partner_name}`
и `./amenities_mapping_codegen {partner_name}`
Это создаст в папке вашего фидера файлы 
features_mapping.py
hotel_type_mapping.py
rubrics_mapping.py

Тулзы требуют подключения к yt для загрузки снэпшота справочника и построения актуальных списков и маппингов фичей.

Иногда бывают проблемы с кодировками, поэтому можно использовать helpers.to_unicode для словарей
и helpers.format_to_text для ворнингов
https://a.yandex-team.ru/arc/trunk/arcadia/travel/hotels/feeders/lib/helpers.py

Нужно маппить признаки которые типично называются themes, amenities, features. <br>
themes - "пляжный отель", "горнолыжный курорт" и т.п.<br>
amenitites/features - "wifi", "бассейн", "бесплатный трансфер"


### Мердж переводов, translations

Некоторые фиды скачиваются на нескольких языках и в конце мерджатся
Это вынесенно в общий класс Partner и настраивается следующим образом
```
langs_map = {  # assume that first language is the main.
    "ru": ['ru', 'en'],
    'default': ['en', 'ru']
}
allowed_languages = ["en", "ru"]
languages = [l for l in list(set().union(*six.itervalues(langs_map))) if l in allowed_languages]
merge_dict_fields = base.Partner.merge_dict_fields + ["photos", ]
merge_localized_fields = base.Partner.merge_localized_fields + ['_ostrovokPolicies', ]
merge_translations = True
```

### Добавить в фидер package.json - в двух местах!
`arcadia/travel/hotels/feeders/package.json`<br>
- [ ] "build": { "targets": [ # https://a.yandex-team.ru/arc/trunk/arcadia/travel/hotels/feeders/package.json#L8
- [ ] "data": [ # https://a.yandex-team.ru/arc/trunk/arcadia/travel/hotels/feeders/package.json#L25

### Релиз package
После коммита начнется автосборка пакета в сэндобксе. <br>
Об этом придет сообщение в канал travel-build в slack.
В сообщении будет ссылка на страничку build таски в сэндбоксе
После завершения сборки И автовыкатки в тестинг нужно нажать кнопку "release" (с галочкой) и зарелизить с дефолтной опцией "stable".
После выкатки в stable пакет станет доступен для использования.

### Добавить teamcity таску
Добавляем процесс в teamcity по шаблону "travel"<br>
Привожу инструкцию и как туда попадать через интерфейс, и прямые ссылки<br>
На [страничке проекта travel в teamcity](http://teamcity/project.html?projectId=Travel&tab=projectOverview)<br>
По кнопочке `edit project settings` справа сверху попадаем [сюда](http://teamcity/admin/editProject.html?projectId=Travel) 
В разделе subprojects идем в [feeders](http://teamcity/admin/editProject.html?projectId=Travel_Feeders)
Кнопка `Create build configuration`<br>
заполнить поле name - название фидера <br>
В dropdown списке `Based on template` выбрать пункт с неординарным названием "Template"<br>

#### Параметры. 
После выбора template-а появятся параметры. Нужно заполнить два:
- [ ] partner.name - название вашего **//sandbox package//**
- [ ] partner.args - аргументы командной строки. Обычно это секрет-пароль. Он указывается в следующем виде: 

`partner.name` - имя фидера<br>
`partner.args` - параметры командной строки. 
`--password "%secret.partner.{partner_name}.password%"` <br>
Чтобы передавать секретное значение нужно его добавить в параметры проекта (см ниже)<br>

Добавляем секреты в teamcity
- [ ] Открываем любой фидер ((http://teamcity/viewType.html?buildTypeId=Travel_Feeders_Booking21)) 
-> **Edit configuration settings** (правый верхний угол) -> **parameters** -> secret.partner.{partner_name}.password 
смотрим откуда оно inherited, идем туда - проект Travel в верхней строчке, 
там снова `parameters`, и добавляем по аналогии с остальными.

#### Запуск
- [ ] Не забыть зарелизить пакет в сэндбоксе
Нажать кнопочку run в строчке с новым фидером на [страничке в тимсити](https://teamcity.yandex-team.ru/project.html?projectId=Travel_Feeders)
- [ ] Не забыть Schedule Trigger в тимсити для запуска каждый день


### Добавление фида в алтай
**Перед тем, как продолжать, необходимость связаться с @ritapak и показать ей тот фид, что получился в YT. Первичную проверку этих данных стоит делать до загрузки в Алтай**

1. Если это новый партнер - сделать нового поставщика в алтае с названием `ytravel_{partner_name}` <br>
Если поставщик уже существует то взять его.

2. Нужно добавить фиды в поставщика
Для этого использовать тулзу https://a.yandex-team.ru/arc/trunk/arcadia/travel/hotels/feeders/scripts/update_altay_configs/
Конфиги для этой тулзы лежат в папочке partners_settings в формате json
1 элемент - 1 фид. У нас обычно 4 фида (russia_hotels, russia_apartments, world_hotels, world_apartments)

Можно скопировать какой-нибудь уже имеющийся конфиг. <br>
Поправить provider_id на id поставщика (ytravel_{partner}) - число со странички в алтае <br>
Удалить "id" потому что иначе вы замените другие конфиги <br>
Сначала всем фидам нужно поставить настройку draft. <br>
Подробное описание всех настроек лежит в README <br>
Все необязательные настройки можно оставить незаполненными и им будет присвоено значение по умолчанию 
(то, которое мы считаем уместным на данный момент)

Дальше нужно сбилдить и запустить тулзу передав ей путь до вашего settings файла <br>
`./update_altay_configs partners_settings/dolphin.json commit`

В алтае зайти на страничку фида и нажать кнопку "проверить" чтобы убедиться что данные загружаются

3. Если фид большой - больше 10000 элементов - и может существенно пошатать базу, 
то нужно завести через Полину @svyatokum эксп на добавление чтобы посмотреть что произойдет

Если небольшой то можно сразу катить в прод - убрать draft, выставить enabled=true и закоммитить заново.


### FAQ & tips

Когда допускается отсутствие значения - явная проверка не нужна
`hotel.{field} = dict_item.get('{field}'})` - ок. (None handled properly)
`hotel.{field}.add(value = dict_item.get('{field}'})`, lang={lang}) - не ок. (нужно if-ом проверять что значение есть)

#### Helpers

`helpers.format_to_text()` - использовать при выводе ворнингов (иначе на русском тексте может упасть с ошибкой)

`helpers.wrap_into_list(val):` <br>
`val if isinstance(val, list) else [val,]` <br>
если значение поля бывает списком - стоит обернуть.<br> 
Иначе если партнер вместо списка передаст единственный элемент (строку) - будет итерация по ней.  