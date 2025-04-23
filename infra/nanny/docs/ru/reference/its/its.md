# Instance Tune System

## О сервисе
### Что это?
**ITS** – система оперативного управления настройками инстансов. ITS не гарантирует консистентность.

### Как она работает?
* В ITS прописываются правила, задающие значения (в какой файл и что записать) для определённых инстансов (которые задаются фильтром с синтаксисом [калькулятора Блинова](https://doc.yandex-team.ru/generated/skynet/sky/blinovcalc.html), поддерживаемые тэги: `I@` и `f@`).
* Клиент (обычно это instancectl) периодически связывается с ITS и получает словарь значений (имя файла — содержимое файла) со значениями параметров инстанса.
Файлы этих ручек он сохраняет в поддиректорию инстанса `controls`. Программа, запущенная instancectl'ем, должна знать, где лежат её ручки, и периодически проверять их обновления.

###  Какие даёт гарантии? {#guarantees}
* Гарантии доставки: best effort
Система не гарантирует верхний предел - "данные когда-нибудь доедут".
* Гарантии консистентности доставки нет.
То есть, сервис не даёт гарантии, что «ваши данные доехали до всех живых инстансов и больше никто не получит старые данные». Вместе с тем, в рамках одного инстанса апдейты данных монотонны: если мы получили более свежую конфигурацию, то бекенд на старую конфигурацию больше не откатится (если не потеряет стейт из-за, например, переналивки);
* Консистентность данных на бекендах ITS гарантируется MongoDB;
* Доставка осуществляется периодическим опросом ITS для получения новых данных:
Период опроса настраивается и может выставлен, например, в 10 секунд.
* Статистика в UI:
    * Количество розданных значений верно до тех пор, пока не "портится" стейт инстансов на машине (например, из-за переналивки хоста);


### Как встроить поддержку ITS в программму
[Для C++](https://wiki.yandex-team.ru/DmitrijjZacepin/AntiFuckupCgi)

### Что ещё нужно?
Нужен клиент, получающий значения ручек из ITS. На данный момент их два:

* **instancectl** - версии 1.2.12 или новее.
Как включить получение ручек в instancectl описано [здесь](https://wiki.yandex-team.ru/jandekspoisk/sepe/instancectl/#its-support).
* Отдельный [its_client](https://bb.yandex-team.ru/projects/NANNY/repos/its_client/browse).
Как его использовать описано [здесь](https://bb.yandex-team.ru/projects/NANNY/repos/its_client/browse/README.md).

##  Администраторам {#admin-guide}

* [Расположение/доступ/балансировщики](admin-info.md)

##  Конфигурирование {#configuration}
###  Глоссарий {#glossary}

**Ручка** — настройка, которая применима к некоторому множеству инстансов.
**Конфиг ручки** задаёт путь к файлу в директории controls, способы валидации и форматирования значений, вводимых пользователям, и так далее.
**Валидатор** — функция, валидирующая введённые пользователем значения. Определяется в исходном коде ITS.
**Процессор** — функция, добавляющая семантику к пользовательским значениям. Определяется в исходном коде ITS.
**Функция склейки** — функция, склеивающая значения нескольких ручек. Определяется в исходном коде ITS.
**Форматтер** — функция, форматирующая значение, полученное от процессора. Результат будет записан в файл в директории `controls`. Определяется в исходном коде ITS.
**Локация** описывает конкретный набор инстансов и применимые к ним ручки, например:

```
filter: I@a_itype_base . I@a_prj_video-main . I@a_geo_sas . I@a_ctype_prestable
ruchkas:
  - degrade
responsible: ['nekto0n', 'romanovich']
```
**Группа** — средство иерархически упорядочить локации. Группа может содержать либо другие группы, либо локации, например:

```
groups:
  msk: <локация или группа>
  sas: <локация или группа>
```

Важно, что все дочерние элементы группы должны быть одного типа — либо локации, либо группы, то есть, в приведённом примере `msk` не может быть группой, если `sas` — локация.

###  Подробнее о том, почему всё так сложно {#why-so-complicated}

Немного о том, зачем нужны валидаторы, форматтеры, процессоры и функции склейки.

Положим, у сервиса есть параметры, которые он читает из файла в виде URL-encoded query string (`field_1=...&field_2=...&field_3=...`).
В самом простом случае ITS может быть объявлена ручка-мультиселект, в которой можно выбрать, какие из `field*` должны содержать истинные значения.
Пользовательское значение будет списком `["field_1", "field_2"]`. Валидатор должен проверить, что все элементы списка допустимы. Процессор, знающий о семантике ручки, должен превратить пользовательский список в список пар `[["field_1", "yes"], ["field_2", "yes"]]`. Форматтер должен закодировать этот список в query string.

В несколько более сложном случае нам захочется сделать так, чтобы `field_3` задавался отдельной ручкой в ITS, которая была бы чекбоксом. В таком случае пользовательское значение для этой ручки будет уже скаляром, булевой переменной. Валидатор должен просто проверить её тип. Процессор должен вернуть список вида `[["field_3", "yes"]]`, если пользовательское значение истинно, и пустой список в противном случае. Форматтер — тот же самый, что и у первой ручки.

Теперь, если обе ручки имеют значения (выбраны опции в мультиселекте и нажата галочка), возникает необходимость склеить значения ручек (подразумевается, что для обеих ручек указан один и тот же выходной файл). Склейка производится над данными, полученными от процессоров, и в данном случае сводится к простой конкатенации списков.

Отформатированное значение передаётся луп-скрипту, который без изменений записывает его в файл.

Немного о том, как появилась подобная схема: [https://st.yandex-team.ru/SWAT-1165](https://st.yandex-team.ru/SWAT-1165)

###  Уведомления о забытых ручках {#forgotten-values-notifications}
Через `values_lifetime` (ныне выставлена в 10 часов) после включения ручки ITS начинает рассылать SMS- и email-уведомления, получателями которых являются человек, включивший ручку, и ответственные за локацию, для которой была включена ручка.

Для отдельных ручек можно отключать уведомления, указав `is_permanent: true` в конфиге ручки (см. ниже).

###  Формат конфига ITS {#its-config-format}

ITS конфигурируется в [интерфейсе Няни](https://nanny.yandex-team.ru/ui/#/its/).
Конфигурационный файл представляет собой YAML, содержащий следующие значения.

`acl`: список ACL-записей;
`locations`: должна описывать группу глубиной 2 или 3 уровня;
`ruchkas`: список конфигов ручек, которые могут быть назначены локациям;
`mergers`: список конфигов функций склейки;
`max_age`: целое число — количество секунд, определяющее период, с которым инстансы ходят за новыми значениями в ITS;
`values_lifetime`: целое число — количество секунд, определяющее период, через который значение ручки считается просроченным. Если ручка не является перманентной, и с момента последнего присваивания ей значения прошло более `values_lifetime` секунд, тому, кто выставил просроченное значение, а также ответственным за локацию, в которой была выставлена ручка, начнут приходить email- и SMS-уведомления.

####  ACL {#its-config-format-acl}

Права на **редактирование фильтров ручки** прописываются в [https://nanny.yandex-team.ru/ui/#/permissions/its/](https://nanny.yandex-team.ru/ui/#/permissions/its/) - их нужно отдельно запрашивать у команды Nanny.

Права на **изменение значений ручек** прописываются в ACL, указываемом в конфиге ITS.
В поле `acl` конфига содержится список следующего вида:

```
acl:
  - mask: "base/msk/*"
    logins:
      - romanovich
      - nekto0n
    groups:
      - yandex_mnt_sa_runtime_auto  # staff group
      - svc_search-wizard_administration  # abc service
```

Когда пользователь делает запрос на изменение или удаление значения ручки, путь ручки (например, `base/msk/degrade`, где `base/msk` — путь локации, а `degrade` — идентификатор ручки) прогоняется по указанным в ACL маскам. Если пользователь присутствует в списке логинов или состоит в одной из групп, указанных в ACL со сматчившейся маской, запрос будет разрешён.

##### Синтаксис масок {#its-config-format-cal-masks}
Маска — slash-separated строка, в которой один или более сегментов могут быть заменены на `*` или `**`. `*` не матчит слэши, в отличии от `**`. Примеры:

* `**` матчит все пути (`a`, `a/b`, `a/b/c` и так далее);
* `**/z` матчит пути, последний сегмент которых равен `z`: `a/z`, `a/b/z` и так далее;
* `**/z/**` матчит пути, содержащие сегмент `z` в середине: `a/z/b`, `a/z/b/c` и так далее, но не `z/a` и `a/z`;
* `*/a/b` матчит пути из трёх сегментов, заканчивающиеся на `a/b`. Например: `y/a/b`, `z/a/b`;
* `*/a/*` матчит пути из трёх сегментов, у которых второй сегмент равен `a`.

#### Фильтры в ruchkas
В **ITS** для определения тех инстансов, что получат значение ручки, задаётся с помощью фильтров.
Особенности фильтров:

* задаются с помощью выражений [калькулятора Блинова](https://doc.yandex-team.ru/generated/skynet/sky/blinovcalc.html)
* используются только [авто-теги](https://wiki.yandex-team.ru/JandeksPoisk/Sepe/Tegi/). Это такие теги, которые начинаются с `a_` Например: **a_ctype_prestable**, **a_itype_apphost**.
* единственные поддерживаемые тэги фильтра Блинова: `I@` и `f@`.

####  Конфиг функции склейки {#mergers}
Конфиг функции склейки — словарь, содержащий следующие ключи:

`path` — путь к файлу относительно директории `controls`. Значения ручек, пишущих в этот файл, будут подвергнуты склейке;
`merger` — имя функции склейки;
`settings` — словарь с настройками, который будет передан функции склейки.

#####  Функции склейки {#mergers-list}
* `concat_merger` — конкатенирует значения, будь то списки, строки или словари;
* `join_merger` — соединяет значения-строки, используя разделитель, указанный в `settings.separator`.
* `key_values_merger` — объединяет key-value списки, соединяя значения совпадающих ключей, используя разделитель, указанный в `settings.separator`. Например:

```python
key_values_merger([
  [('rearr', 'a,b')],
  [('rearr', 'c')]
], {'settings': {'separator': ','}})```
вернёт `[('rearr', 'a,b,c')]`.
```

* `outer_params_merger` — см. [https://st.yandex-team.ru/SWAT-2048#1443512073000](https://st.yandex-team.ru/SWAT-2048#1443512073000)
Для соединения пересекающихся outer params, функция берёт сепаратор из настройки `settings.separators.<имя-outer-параметра>`. Если он не указан, параментр не склеивается в один, а повторяется несколько раз (см. [SWAT-2167](https://st.yandex-team.ru/SWAT-2167)).

####  Конфиг ручки {#values-config}

Конфиг ручки — словарь со следующими ключами:

`id` (обязательное) — идентификатор ручки, на который могут ссылаться локации;
`path` (обязательное) — путь к файлу относительно директории `controls`, в который будет положено значение ручки;
`name` — человекочитабельное имя ручки, используется сугубо в UI;
`widget` — определяет, как будет отображаться ручка в UI;
`validator` — имя валидатора;
`processor` — имя процессора;
`formatter` — имя форматтера;
`is_permanent` – если true, значение ручки не будет считаться просроченным никогда;
`settings` — словарь, содержащий данные, специфичные для валидатора и форматтера.

#####  Виджеты {#values-config-widgets}

* `default` — виджет по умолчанию, обычное текстовое поле;
* `select` — поле выбора, допускающее одну выбранную опцию;
* `multiselect` — поле выбора, допускающее несколько выбранных опций;
* `json` — большое текстовое поле с подсветкой и проверкой синтаксиса JSON;
* `multiline` — большое текстовое поле;
* `button` — кнопка, по нажатии на которую ручка принимает заданное значение. «Вырожденный» случай виджета `select` с единственной опцией.

Виджет `button` берёт первое (которое должно быть единственным) значение из поля `settings.choices`, виджеты `select` и `multiselect` также берут список опций из поля `settings.choices`. Оно должно содержать либо список строк, либо список словарей вида `{key: ..., value: ...}`.

#####  Валидаторы {#values-config-validators}

* `noop` — (выставлен по умолчанию) не делает ничего;
* `choices_validator` — проверяет, то значение присутствует в `settings.choices` [1];
* `multiple_choices_validator` — проверяет, что все значения из предоставленного пользователем списка присутствуют в `settings.choices` [1];
* `float_validator` — проверяет, что значение является числом, возмозможно, дробным. Проверяет, что значение лежит в интервале, заданном настройкой `settings.range` [2];
* `int_validator` — проверяет, что значение является целым числом. Проверяет, что значение лежит в интервале, заданном настройкой `settings.range` [2];
* `json_validator` — проверяет, что значение содержит валидный JSON.

##### Уточнения

1. `settings.choices` должно содержать либо список строк, либо список словарей вида `{key: ..., value: ...}`, где key будет отображаться в качестве человекочитабельного имени;
1. `settings.range` должно содержать список из двух значений, минимального (включительно) и максимального (включительно).

##### Процессоры

* `noop` — (выставлен по умолчанию) не делает ничего;
* `subparam_processor` — принимает на вход скаляр или список (например, `["a", "b", "c"]`) и возвращает список, содержащий единственный элемент — пару ключ-значение (например, `[["key", "a,b,c"]]`). Имя ключа задаётся настройкой `settings.subparam_name`, разделитель значений (в приведённом примере — запятая) задаётся в `settings.subparam_separator`. Также поддерживается `settings.subparam_format`, в котором можно указать шаблон (формат шаблона такой же, как и у `string_formatter`), с помощью которого будет форматироваться значение (в случае, если исходное значение — список, шаблон будет применён к уже скленныму списку, а не к каждому из его элементов по отдельности);
* `json_processor` — принимает на вход JSON-строку и возвращает словарь;
* `outer_param_processor` – историю его возникновения можно узнать в [SWAT-2048](https://st.yandex-team.ru/SWAT-2048).

Обязательные параметры: `outer_param_name`.
Если указан `subparam_name`, возвращает словарь вида `{outer_param_name: [[(subparam_name, subparam_value)]]}`, где `(subparam_name, subparam_value)` — результат `subparam_processor` (логика которого управляется настройками `subparam_name`, `subparam_separator` и `subparam_format`). Пример возвращаемого значения: `{"rearr": [[("imgban_disable", "1,2")]]}`).

Если `subparam_name` не указан, процессор обращается к настройкам `outer_param_separator` и `outer_param_format`, и возвращает словарь вида `{outer_param_name: [[(outer_param_value, "")]]}`, где `outer_param_value` формируется по той же логике, что и `subparam_value`. Пример возвращаемого значения: `{"disable": [[("yes", "")]]}`).
Стоит отметить, что каждому outer param name в результирующем словаре сопоставлен список списков key-value значений. Это сделано для того, чтобы `outer_params_formatter` мог не отличать результат `outer_param_processor` от `outer_param_merger`.

##### Форматтеры

* `noop` — (выставлен по умолчанию) не делает ничего;
* `sepe_8983_formatter` — объединяет и форматирует значения для верхнего поиска. См. [https://st.yandex-team.ru/SEPE-8983](https://st.yandex-team.ru/SEPE-8983).
* `string_formatter` — форматирует значение, используя шаблон `settings.format_string`. Шаблон должен содержать плейсхолдер `s%%`. Важно: `s%%` — единственный поддерживаемый плейсхолдер, никакого printf-подобного функционала форматтер не предоставляет;
* `test_formatter` — добавляет к значению префикс `"test "`;
* `subparam_formatter` — работает идентично одноимённому процессору, только вместо списка из одного элемента возвращает URL-encoded строку, кодирующую единственный параметр;
* `query_string_formatter` — принимает на вход список пар ключ-значение и превращает его в URL-encoded query string `r`. Если указан `settings.param_name`, возвращает URL-encoded пару `(settings.param_name, r)`, в противном случае возвращает `r`;
* `json_formatter` — принимает на вход словарь и кодирует его в JSON;
* `outer_params_formatter` – принимает на вход словарь, ключами которого являются outer param names, а значениями — списки списков пар (ключ, значение). Принцип его работы легче понять на примере: словарь вида `{ 'rearr': [ [('k1', 'a1,a2')], [('k2', '')], ], 'disable_smth': [ [('yes', '')], [('a', 'x'), ('b', 'y')] ], 'pron': [ [('k1', 'a1')] ], }` будет преобразован в строку: `"rearr=k1%3Da1%2Ca2&rearr=k2&disable_smth=yes&disable_smth=a%3Dx%26b%3Dy&pron=k1%3Da1"`, более наглядно: **rearr**=`k1%3Da1%2Ca2`&**rearr**=`k2`&**disable_smth**=`yes`&**disable_smth**=`a%3Dx%26b%3Dy`&**pron**=`k1%3Da1`.

#### Пример валидного конфига

```yaml
locations:
  groups:
    base:
      groups:
        msk:
          groups:
            EngTier0:
              filter: I@a_itype_base . I@a_prj_web-main . I@a_geo_msk . I@a_tier_EngTier0 . I@a_ctype_prod
              ruchkas:
              - degrade
            VideoTier0:
              filter: I@a_itype_base . I@a_prj_video-main . I@a_geo_msk . I@a_ctype_prod
              ruchkas:
              - degrade
        sas:
          groups:
            EngTier0:
              filter: I@a_itype_base . I@a_prj_web-main . I@a_geo_sas . I@a_tier_EngTier0 . I@a_ctype_prestable
              ruchkas:
              - degrade
    wizard:
      groups:
        msk:
          filter: I@a_itype_wizard . I@a_prj_search-wizard . I@a_geo_msk
          ruchkas:
          - wizard
        sas:
          filter: I@a_itype_wizard . I@a_prj_search-wizard . I@a_geo_sas
          ruchkas:
          - wizard
        upper:
          filter: I@a_itype_upper
          ruchkas:
          - upper_flags
          - upper_flags_location
ruchkas:
- id: degrade
  path: ./degrade
  name: Quality
  validator: float_validator
  formatter: string_formatter
  settings:
    format_string: pron=smm_%s
    range:
    - 0.01
    - 1
- id: wizard
  path: ./degrade
  name: Degradation
  validator: choices_validator
  formatter: string_formatter
  settings:
    choices:
    - light
    - superlight
    format_string: rn=%s
- id: upper_flags
  path: ./flags.json
  widget: json
  validator: json_validator
  processor: json_processor
  formatter: json_formatter
  is_permanent: true
- id: upper_flags_location
  path: ./flags.json
  widget: json
  validator: json_validator
  processor: json_processor
  formatter: json_formatter  
  is_permanent: true
mergers:
- path: ./flags.json
  merger: concat_merger
max_age: 60
```

## Как развернуть ITS локально

* Зачекаутить исходный код:

```
git clone ssh://git@git.qe-infra.yandex-team.ru/nanny/its.git
```

* Установить Python-зависимости (желательно в venv):

```
pip install -r ./pip-requirements.txt --index http://pypi.yandex-team.ru/simple/
pip install -r ./pip-requirements-dev.txt --index http://pypi.yandex-team.ru/simple/
```
* Обеспечить наличие mongod в `PATH` (подходящий бинарник можно получить, запустив `sky get -wu rbtorrent:dfa2f740dd7ad21689a9ea367d29e7f72a583327`)
* Прописать пути к существующим логам в `cfg_test.yml`
* Запустить `./test.sh`

## API

ITS предоставляет HTTP API. [http://nanny.yandex-team.ru/ui/#/its/locations/](http://nanny.yandex-team.ru/ui/#/its/locations/) — интерфейс к нему.

Продакшн доступен по адресу [http://its.yandex-team.ru/](http://its.yandex-team.ru/)

### Аутентификация

Все запросы к API сервисов должны быть аутентифицированы. Аутентификация производится через внутренний Паспорт.

* Для запросов из браузера проверяется cookie `Session_id`.
* Для запросов роботами необходимо использовать OAuth токен, добавив его в заголовки запросов: Authorization: OAuth {access_token}

При этом так же будет использована паспортная авторизация.
OAuth-токен пользователя можно получить на странице [http://nanny.yandex-team.ru/ui/#/oauth/](http://nanny.yandex-team.ru/ui/#/oauth/).

#### Формат ответа
Для корректной работы рекомендуется всегда указывать заголовок  `Accept ` со значением  `application/json `. Ответы так же возвращаются в формате JSON.

#### Формат запроса
Все запросы на изменения в своём теле должны передаваться в формате JSON и содержать заголовок  `Content-Type ` со значением  `application/json `.

### Методы

#### Получение значений всех ручек
```
GET /v1/values/ HTTP/1.1
Accept: application/json
Authorization: OAuth <...>
Content-Type: application/json; charset=utf-8

HTTP/1.1 200 OK
Content-Type: application/json

{
"upper_priemka/web_rc/upper_priemka_flags": {
"value": "{}",
"version": "rev_885"
}
}

```

#### Управление значениями ручек
Производится HTTP-запросами к `/v1/values/<location_path>/<ruchka_id>/`.

`location_path` — путь локации в конфиге, например, `base/man/EngTier0` или `mmeta/msk/Images`.
`ruchka_id` – идентификатор ручки, заданный в секции `ruchkas` в конфига.

##### Установка значения

При условии, что значение ручки не было установлено ранее:

```
GET /v1/values/mmeta/man/Images/images_rearrange/ HTTP/1.1
Accept: application/json
Accept-Encoding: gzip, deflate, compress
Authorization: OAuth a483269fa5bf45d9b554ec3f02326cb7
Content-Type: application/json; charset=utf-8
Host: dev-its.yandex-team.ru
User-Agent: HTTPie/0.8.0

HTTP/1.1 404 NOT FOUND
```
Установить его можно следующим POST-запросом.

```
POST /v1/values/mmeta/man/Images/images_rearrange/ HTTP/1.1
Accept: application/json
Authorization: OAuth <...>
Content-Type: application/json; charset=utf-8

{
    "value": "ValueOne"
}

HTTP/1.1 200 OK
Content-Type: application/json
ETag: "rev_17"

{
    "formatted_value": "rearr=ValueOne_off",
    "path": "mmeta/man/Images/images_rearrange",
    "user_value": "ValueOne"
}
```

##### Изменение значения

При условии, что ручка уже была установлена, простой POST-запрос вернёт ошибку.

```
POST /v1/values/mmeta/man/Images/images_rearrange/ HTTP/1.1
Accept: application/json
Authorization: OAuth <...>
Content-Type: application/json; charset=utf-8

{
    "value": "ValueTwo"
}

HTTP/1.1 412 PRECONDITION FAILED
Content-Type: application/json

{
    "message": "value has been modified by another user"
}
```

Чтобы запрос прошёл успешно, необходимо указать предыдущую версию значения (взятую из поля `version`) в заголовке `If-Match`. Такой механизм предотвращает lost updates.

```
POST /v1/values/mmeta/man/Images/images_rearrange/ HTTP/1.1
Accept: application/json
Authorization: OAuth <...>
Content-Type: application/json; charset=utf-8
If-Match: rev_17

{
    "value": "ValueTwo"
}

HTTP/1.1 200 OK
Content-Type: application/json
ETag: "rev_18"

{
    "formatted_value": "rearr=ValueTwo_off",
    "path": "mmeta/man/Images/images_rearrange",
    "user_value": "ValueTwo"
}
```

##### Удаление значения ручки

```
DELETE /v1/values/mmeta/man/Images/images_rearrange/ HTTP/1.1
Accept: application/json
Authorization: OAuth <...>
Content-Type: application/json; charset=utf-8
If-Match: rev_18

{
    "value": "ValueTwo"
}

HTTP/1.1 204 NO CONTENT
```

#### Статистика по свежести ручек

```
GET /v1/statistics/ HTTP/1.1
Accept: application/json
Authorization: OAuth <...>
Content-Type: application/json; charset=utf-8

HTTP/1.1 200 OK
Content-Type: application/json

{
    "balancer/msk/web_kubr": {
        "number_of_instances": 60,
        "ruchkas": {}
    },
    "balancer/sas/web_com": {
        "number_of_instances": 14,
        "ruchkas": {
            "balancer_click_switch": {
                "number_of_times_returned": 14
            }
        }
    },
    "base/man/EngTier0": {
        "number_of_instances": 3132,
        "ruchkas": {
            "base_degrade": {
                "number_of_times_returned": 3093
            }
        }
    },
    "base/man/EngTier1": {
        "number_of_instances": 2376,
        "ruchkas": {
            "base_degrade": {
                "number_of_times_returned": 2348
            }
        }
    },
    "mmeta/sas/Images": {
        "number_of_instances": 41,
        "ruchkas": {
            "images_ban": {
                "number_of_times_returned": 41
            },
            "images_rearrange": {
                "number_of_times_returned": 39
            }
        }
    }
}
```

#### История значений

Доступна по GET-запросу к `/v1/history/<path>/`.

`path` может быть как путём к ручке, так и локации (в таком случае будут возвращены значения всех её ручек).
GET-параметры `limit` и `offset` используются для пагинации.
Значения упорядочены по времени их записи (самые свежие идут первыми).

```
GET /v1/history/balancer/l7_heavy/web_com_l7/search_l7_balancer_switch/?limit=10&skip=0 HTTP/1.1
Accept: application/json
Authorization: OAuth <...>
Content-Type: application/json; charset=utf-8

HTTP/1.1 200 OK
Content-Type: application/json
Date: Fri, 05 Feb 2016 08:11:01 GMT

{
    "result": [
        {
            "author": "nanny-robot",
            "is_deleted": false,
            "location_path": ["balancer", "l7_heavy", "web_com_l7"],
            "ruchka_id": "search_l7_balancer_switch",
            "time": "2016-02-03T16:34:53.151000",
            "user_value": "{\n    \"comment\": \"Pushed by roboslone. DO NOT EVER edit it by hand -- it will break the Nanny UI!\", \n    \"config_version\": \"c18b8266f6a200770586384f468bf74ce6670e21\", \n    \"payload\": {\n        \"search\": {\n            \"SAS\": 34, \n            \"DEVNULL\": 0, \n            \"PUMPKIN\": 0, \n            \"MSK\": 33, \n            \"MAN\": 33\n        }, \n        \"touchsearch\": {\n            \"SAS\": 34, \n            \"DEVNULL\": 0, \n            \"PUMPKIN\": 0, \n            \"MSK\": 33, \n            \"MAN\": 33\n        }, \n        \"blogs\": {\n            \"SAS\": 34, \n            \"DEVNULL\": 0, \n            \"PUMPKIN\": 0, \n            \"MSK\": 33, \n            \"MAN\": 33\n        }, \n        \"misc\": {\n            \"SAS\": 34, \n            \"DEVNULL\": 0, \n            \"PUMPKIN\": 0, \n            \"MSK\": 33, \n            \"MAN\": 33\n        }, \n        \"touchlogs\": {\n            \"SAS\": 34, \n            \"DEVNULL\": 0, \n            \"PUMPKIN\": 0, \n            \"MSK\": 33, \n            \"MAN\": 33\n        }, \n        \"video\": {\n            \"SAS\": 34, \n            \"DEVNULL\": 0, \n            \"PUMPKIN\": 0, \n            \"MSK\": 33, \n            \"MAN\": 33\n        }, \n        \"cycounter\": {\n            \"SAS\": 34, \n            \"DEVNULL\": 0, \n            \"PUMPKIN\": 0, \n            \"MSK\": 33, \n            \"MAN\": 33\n        }, \n        \"images\": {\n            \"SAS\": 34, \n            \"DEVNULL\": 0, \n            \"PUMPKIN\": 0, \n            \"MSK\": 33, \n            \"MAN\": 33\n        }, \n        \"portal\": {\n            \"TEST\": 0, \n            \"MSK\": 34, \n            \"SAS\": 33, \n            \"DEVNULL\": 0, \n            \"MAN\": 33, \n            \"PUMPKIN\": 0\n        }, \n        \"searchapp\": {\n            \"SAS\": 34, \n            \"DEVNULL\": 0, \n            \"PUMPKIN\": 0, \n            \"MSK\": 33, \n            \"MAN\": 33\n        }\n    }\n}"
        },
        ...
    ]
}
```

#### Управление конфигом ITS

Путь к секции конфига представляет собой строку, разделённую слешами. Пути к секциями с ручками или функциями склейки обозначаются строками `ruchkas` и `mergers` соответственно. Путь к локации можно увидеть в адресной строке, открыв её в браузере: [https://dev-nanny.yandex-team.ru/ui/#/its/locations/experiments/sas/](https://dev-nanny.yandex-team.ru/ui/#/its/locations/experiments/sas/). В данном случае путь к секции конфига будет `locations/experiments/sas`.

##### Получение конфига

ITS предоставляет метод для получения конфига или некоторых его секций.
Метод доступен по GET-запросу к `/v2/config/current/` (для получения всего конфига) или `/v2/config/current/<config_path>/` (для получения секции `config_path`).

Вызов вернёт словарь с двумя полями, `version` и `content`, где `version` — текущая версия **всего** конфига (даже в случае получения секции), а `content` — содержимое всего конфига или его секции.

```
GET /v2/config/current/locations/upper/man/ HTTP/1.1
Accept: application/json
Authorization: OAuth <...>
Content-Type: application/json; charset=utf-8

HTTP/1.1 200 OK
Content-Length: 507
Content-Type: application/json
Date: Wed, 04 May 2016 07:12:36 GMT
{
    "content": {
        "groups": {
            "Images": {
                "filter": "I@a_itype_upper . I@a_prj_imgs-main . I@a_geo_man",
                "responsible": [
                    "robot-searchmon"
                ],
                "ruchkas": [
                    "upper_flags",
                    "upper_cgi_params"
                ]
            },
            "Web": {
                "filter": "I@a_itype_upper . [ I@a_prj_web-main I@a_prj_web-comtr I@a_prj_web-com ] . I@a_geo_man",
                "responsible": [
                    "robot-searchmon"
                ],
                "ruchkas": [
                    "upper_flags",
                    "upper_flags_location",
                    "upper_degrade",
                    "upper_disable_cached",
                    "upper_its_touch_granny",
                    "upper_cgi_params"
                ]
            }
        }
    },
    "version": "56eca1d377dd479617097e4e"
}
```

##### Изменение конфига

Изменить конфиг или его секцию можно с помощью POST-запроса по адресу `/v2/config/current/<config_path>/`. Запрос должен JSON-словарь с двумя полями, `version` и `content`, где `version` — текущая версия **всего** конфига, а `content` — содержимое конфига или его секции.

```
POST /v2/config/current/locations/upper/ HTTP/1.1
Accept: application/json
Authorization: OAuth <...>
Content-Type: application/json; charset=utf-8

{
    "version": "5729b4213acdeb0755488e14",
    "content": {
        "groups": {
            "Images": {
                "filter": "I@a_itype_upper . I@a_prj_imgs-main . I@a_geo_man",
                "responsible": [
                    "robot-searchmon"
                ],
                "ruchkas": [
                    "upper_flags"
                ]
            }
        }
    }
}

HTTP/1.1 200 OK
Content-Length: 507
Content-Type: application/json
Date: Wed, 04 May 2016 08:43:30 GMT

{
    "version": "5729b62fb0d42e08034d8ff3",
    "content": {
        "groups": {
            "Images": {
                "filter": "I@a_itype_upper . I@a_prj_imgs-main . I@a_geo_man",
                "responsible": [
                    "robot-searchmon"
                ],
                "ruchkas": [
                    "upper_flags"
                ]
            }
        }
    }
}
```

## Разное

### Протокол взаимодействия потребителей ручек с ITS

На данный момент потребитель ручек один — [loop-скрипт](https://git.qe-infra.yandex-team.ru/projects/NANNY/repos/instance-loop/browse).
Потребитель периодически обращается к API ITS, чтобы получить словарь, ключами которого являются имена, а значениями — содержимые файлов с ручками.

Метод `/v1/process/` принимает POST-запрос со списком instance-тегов и возвращает словарь значений ручек. И запрос, и ответ закодированы в JSON.

Первый запрос потребителя к ITS выглядит следующим образом:

```
POST /v1/process/ HTTP/1.1
Accept: application/json
Content-Length: 80
Content-Type: application/json; charset=utf-8
Host: its.yandex-team.ru

[
    "a_itype_balancer",
    "a_prj_imgs-main-thumb",
    "a_geo_sas",
    "a_ctype_prestable"
]
```

```
HTTP/1.1 200 OK
Cache-Control: max-age=60
Content-Length: 217
Content-Type: application/json
Date: Fri, 08 May 2015 07:31:25 GMT
ETag: "1431070200000:eyJ0aHVtYm5haWxzL2ltZ3NfaW1wcm94eS9zYXMiOiB7ImJhbGFuY2VyX2ltcHJveHlfaW1nZnRoX3dlaWdodHMiOiAiNTU0NDhhODE2MjRhN2YwMWU3YjEyZjFkIiwgImJhbGFuY2VyX2ltcHJveHlfaW1nc3RoX3dlaWdodHMiOiAiNTUzOWQ5ZmI4YThhZTE3YWNlODU2Y2I1IiwgImJhbGFuY2VyX2ltcHJveHlfY2FjaGVyX3dlaWdodHMiOiAiNTU0MjNjMDU0ZGNlNGE3OWEzMTdmODljIn19"

{
    "./cacher.weight": "localhost_cacher,0\nsas_cacher,1",
    "./imgfth.weight": "msk_imgfth,100\nsas_imgfth,0\nsas_nidx_imgfth,0\nmsk_nidx_imgfth,0",
    "./imgsth.weight": "msk_imgsth,0\nsas_imgsth,100\nman_imgsth,0"
}
```

Стоит обратить, что ITS кроме словаря ручек вернул также заголовки `ETag` и `Cache-Control`.
Возвращённый етаг идентифицирует значение ручек и **должен** быть передан во всех последующих запросах в качестве заголовка `If-None-Match`. Этот механизм снижает объём трафика и обеспечивает возможность подсчёта статистики на стороне ITS.

Значение `max-age` в `Cache-Control` содержит количество секунд, через которое клиенту **рекомендуется** перезапросить значения.

Пример запроса с етагом:

```
POST /v1/process/ HTTP/1.1
Accept: application/json
Accept-Encoding: gzip, deflate, compress
Content-Length: 80
Content-Type: application/json; charset=utf-8
Host: its.yandex-team.ru
If-None-Match:  "1431070200000:eyJ0aHVtYm5haWxzL2ltZ3NfaW1wcm94eS9zYXMiOiB7ImJhbGFuY2VyX2ltcHJveHlfaW1nZnRoX3dlaWdodHMiOiAiNTU0NDhhODE2MjRhN2YwMWU3YjEyZjFkIiwgImJhbGFuY2VyX2ltcHJveHlfaW1nc3RoX3dlaWdodHMiOiAiNTUzOWQ5ZmI4YThhZTE3YWNlODU2Y2I1IiwgImJhbGFuY2VyX2ltcHJveHlfY2FjaGVyX3dlaWdodHMiOiAiNTU0MjNjMDU0ZGNlNGE3OWEzMTdmODljIn19"
User-Agent: HTTPie/0.8.0

[
    "a_itype_balancer",
    "a_prj_imgs-main-thumb",
    "a_geo_sas",
    "a_ctype_prestable"
]
```

Ответом может быть как 200 (пример приведён выше), так и 304, что означает, что ни етаг, ни значения не изменились:

```
HTTP/1.1 304 NOT MODIFIED
Cache-Control: max-age=60
Date: Fri, 08 May 2015 07:38:00 GMT
ETag: "1431070200000:eyJ0aHVtYm5haWxzL2ltZ3NfaW1wcm94eS9zYXMiOiB7ImJhbGFuY2VyX2ltcHJveHlfaW1nZnRoX3dlaWdodHMiOiAiNTU0NDhhODE2MjRhN2YwMWU3YjEyZjFkIiwgImJhbGFuY2VyX2ltcHJveHlfaW1nc3RoX3dlaWdodHMiOiAiNTUzOWQ5ZmI4YThhZTE3YWNlODU2Y2I1IiwgImJhbGFuY2VyX2ltcHJveHlfY2FjaGVyX3dlaWdodHMiOiAiNTU0MjNjMDU0ZGNlNGE3OWEzMTdmODljIn19"
```

В случае, если потребитель хочет получить словарь ручек до истечения max-age или смены етага, он должен добавить в запрос заголовок `Expect: 200-ok`.

### Механизм подсчёта статистики

Каждому значению (или его отсутствию) ручки присваивается ревизия — уникальная строка.

Етаг, возвращаемый методом `/v1/process/`, однозначно идентифицирует набор значений инстанса в текущем периоде.
В случае, если меняется текущая ревизия одного значений или наступает новый период, етаг изменяется, и, как следствие, любой запрос (и с `If-None-Match`, и без него) вернёт 200. На этом свойстве и основывается механизм подсчёта статистики.

ITS оперирует понятием периода.
Период имеет начало, конец и хранит информацию о том, сколько раз какая ревизия какого значения была отдана в составе ответа с кодом 200, что (при условии корректного поведения потребителей) эквивалентно количеству потребителей, до которых было доставлено значение.
Длина периода зависит от значения `max_age`, указанного в конфиге. На данный момент это `10 * max_age`.
Не углубляясь в детали реализации, можно сказать, что ITS хранит данные о двух периодах: о текущем и о последнем завершимся.

Статистика значения определяется следующим образом:

* если текущая ревизия была создана в текущем периоде, возвращается количество потребителей из него;
* если текущая ревизия была создана ранее, возвращается максимум из количеств потребителей из текущего и последнего завершившегося периодов.

