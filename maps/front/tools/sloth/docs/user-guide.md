<h1>Пользовательская документация</h1>

- [Вам понадобятся](#вам-понадобятся)
- [Как начать](#как-начать)
  - [Настройка доступов в Testpalm и Бронировщике](#настройка-доступов-в-testpalm-и-бронировщике)
  - [Настройка Hitman](#настройка-hitman)
  - [Настройка Реактора](#настройка-реактора)
    - [Доступ](#доступ)
    - [Измените пути до артефактов в реакциях](#измените-пути-до-артефактов-в-реакциях)
    - [Структура конфига](#структура-конфига)
  - [Настройка Трекера](#настройка-трекера)
    - [Доступы](#доступы)
    - [Клонирование воркфлоу](#клонирование-воркфлоу)
    - [Создание типа задачи](#создание-типа-задачи)
    - [Настройка полей очереди](#настройка-полей-очереди)
    - [Настройка триггеров](#настройка-триггеров)
    - [Синхронизация компонентов](#синхронизация-компонентов)
- [Использование](#использование)
  - [Общий флоу](#общий-флоу)
    - [Работа с тикетом](#работа-с-тикетом)
    - [Если вы хотите внести изменения в тикет](#если-вы-хотите-внести-изменения-в-тикет)
  - [Фильтрация кейсов строкой expression](#фильтрация-кейсов-строкой-expression)
    - [Синтаксис](#синтаксис)
  - [Продвинутая фильтрация по сущностям тестпалма с помощью полей](#продвинутая-фильтрация-по-сущностям-тестпалма-с-помощью-полей)
  - [Кастомизация](#кастомизация)

## Вам понадобятся

1. Доступ к настройкам очереди в трекере
2. Свободный тип задачи "Тестирование"
3. Проект и квота в Testpalm
4. Проект в Реакторе
5. Проект в Хитмане с процессом запуска асессоров

## Как начать

### Настройка доступов в Testpalm и Бронировщике

Выдать [Подрику](https://staff.yandex-team.ru/zomb-podrick) доступы:

**Super tester в IDM для вашего проекта в Testpalm**

</p></details><details><summary><b>Скрин</b></summary><p>

![./pics/Untitled.png](./pics/Untitled.png)

---

</p></details>

**Доступ к источнику квоты с ролью User в Бронировщике**

</p></details><details><summary><b>Скрин</b></summary><p>

![./pics/Untitled%201.png](./pics/Untitled%201.png)

---

</p></details>

### Настройка Hitman

Откройте процесс, который запускает асессоров через Hitman. В список "Ответственные за процесс" нужно добавить [Подрика](https://staff.yandex-team.ru/zomb-podrick), в описании проекта в графе "Пользователь Нирваны", указать [robot-yang-testing](https://staff.yandex-team.ru/robot-yang-testing)

В параметрах графа нужно поменять значения полей:

- booking_id = _.VAR_BOOKING_ID
- parent_ticket = _.VAR_PARENT_TICKET
- special_condition = _.VAR_SPECIAL_CONDITION
- tickets_queue = _.VAR_QUEUE
- version = _.VAR_VERSION
- webhooks_potato_url = _.VAR_WEBHOOK_POTATO_URL
- test_stend = _.VAR_STAND_URI
- Параметр webhooks_via_vanilla с типом Константа и значением true 
- Параметр is_check_required со значением false
- Параметр is_report_required со значением false
- Параметр is_report_show_cost_rub_required со значением true
- Параметр is_report_write_to_ticket_required со значением true

На скриншоте ниже отображен граф со всеми выставленными параметрами, при настройке посмотрите все ли параметры выставлены у Вас аналогично, за исключением индивидуальных параметров проекта(namespace, parent_namespace, project_name, etc)
</p></details><details><summary><b>Скрин</b></summary><p>

![./pics/hitman.png](./pics/hitman.png)

---

</p></details>

**ВАЖНО:** Поддержан автопроброс параметра requester_code. Задайте в своем Хитман процессе ему тип Groovy-функция, укажите значение _.VAR_REQUESTER_CODE. Этот параметр необходимо указывать в паре с параметром requester_code_explanation, чтобы не получить ошибку запуска. При необходимости установки данных параметров прежде всего ознакомьтесь с документацией этих параметров. Для проброса параметра в Хитман процесс создайте в Трекере в категории "Тестирование асессорами" строковое поле с ключом поля - requester_code, подробнее про настройку полей очереди читай в пункте [Настройка полей очереди](#настройка-полей-очереди).

**Добавьте триггер запуска через API Хитмана**
</p></details><details><summary><b>Скрин</b></summary><p>

![./pics/Untitled%203.png](./pics/Untitled%203.png)

---

</p></details>

### Настройка Реактора

Перед настройкой реактора обратитесь к нам за созданием вашей личной папки проекта, в которой у вас будут права на создание/редактирование реакций, папка будет раполагаться в реакторе [`/maps/front/maps/sloth`](https://reactor.yandex-team.ru/browse/resolve?path=/maps/front/maps/sloth). Поле этого продублируйте в ней реакции и артефакты из папки [`example`](https://reactor.yandex-team.ru/browse/resolve?path=/maps/front/maps/sloth/example). Создавать сущности можно нажав на **+** рядом с полем поиска, реакции можно склонировать из папки Example(кнопка "More actions"->"Clone") и затем поменять пути в параметрах своей реакции.

</p></details><details><summary><b>Скрин</b></summary><p>

![./pics/reactor_add_screen.png](./pics/reactor_add_screen.png)

---

</p></details>

#### Доступ

Для каждого созданного артефакта/реакции нужно дать права `Write` для [Подрика](https://staff.yandex-team.ru/zomb-podrick).

Для этого нужно кликнуть на иконку `👑 Owner` в правом верхнем углу на странице сущности (папки/реакции/артефакта)

</p></details><details><summary><b>Скрин</b></summary><p>

![./pics/Untitled%205.png](./pics/Untitled%205.png)

![./pics/Untitled%206.png](./pics/Untitled%206.png)

---

</p></details>

#### Измените пути до артефактов в реакциях

```jsx
var stIssue = a'/maps/front/maps/sloth/ВАШ_ПРОЕКТ/launch-assessors/launch-assessors_artifact'.triggered.data;
var config = a'/maps/front/maps/sloth/ВАШ_ПРОЕКТ/config'.last.data;
```
После создания всех реакций выполните клик в кнопку Activate в интерфейсе каждой реакции.
Добавьте конфиг для ваших проектов в артефакте `/maps/front/maps/sloth/ВАШ_ПРОЕКТ/config`.

#### Структура конфига

```js
{
    "JSAPI v1.1": { // Название вашего проекта
        "queue": "ASESSORSMAPSAPI", // Очередь, в которой асессоры будут заводить баги
        "testpalm_project_id": "maps-js-api-v1-x", // ID проекта в Testpalm
        "testpalm_quota": "qs_testpalm_separate_maps-api_ru", // Квота в Testpalm
        "hitman_trigger": "js-api-v1-x", // ID триггера в Hitman (https://hitman.yandex-team.ru/projects/ВАШ_ПРОЕКТ/ЭТО_ID_ТРИГГЕРА)
        "regular_booking_uuid":"b87c50cf-ff7a-4618-a0dc-661d03fc5fg" // uuid вашей регулярной брони(если регулярной брони нет, просто не указывайте этот параметр в конфиге)
    }, // Таких проектов может быть несколько
}
```

В строковых артефактах реактора есть ограничения на количество символов. Чтобы минифицировать конфиг, после завершения его редактирования в текстовом редакторе, скопируйте и вставьте его в консоль браузера, затем выполните: `const config = *Ваш конфиг здесь*; copy(JSON.stringify(config));`

Это минифицирует его в одну строку и после выполнения команды он будет в вашем буфере обмена.

Перейдите на страницу артефакта вашего конфига и нажмите в интерфейсе `Instantiate` для создания нового инстанса конфига. Вставьте ваш конфиг в поле `Value`

### Настройка Трекера

#### Доступы

Для начала нужно дать доступ роботам. Для этого нужно перейти в редактирование настроек очереди: https://st.yandex-team.ru/НАЗВАНИЕ_ВАШЕЙ_ОЧЕРЕДИ
</p></details><details><summary><b>Скрин - Настройки очереди</b></summary><p>

![./pics/Untitled%207.png](./pics/Untitled%207.png)

---

</p></details>

Здесь находится переход в настройки очереди. Этот попап появляется при нажатии на шестеренку рядом с названием очереди

Выберите пункт "Доступ" в сайдбаре слева и добавьте [Робот Тестировщик](https://staff.yandex-team.ru/robot-yang-testing) и [Подрик Пейн](https://staff.yandex-team.ru/zomb-podrick) с правами, указанными на скриншоте ниже.

Робот Тестировщик будет отправлять в тикет отчет проверке релиза асессорами. Подрик Пейн будет отвечать за автоматизацию процессов.
</p></details><details><summary><b>Скрин - права роботов в очереди</b></summary><p>

![./pics/Untitled%208.png](./pics/Untitled%208.png)

---

</p></details>

#### Клонирование воркфлоу

В сайдбаре слева выберите пункт "Воркфлоу", затем нажмите "Скопировать воркфлоу из другой очереди". В верхнее поле введите ASESSORSMAPSAPI:MAPSAPI-ASESSORS, во втором Релиз на асессоров v2, в нижнем удобное для вас имя воркфлоу. 
</p></details><details><summary><b>Скрин - копирование ворфлоу</b></summary><p>

![./pics/Untitled%209.png](./pics/Untitled%209.png)

---

</p></details>

После клонирования воркфлоу поменяйте условия переходов "Запланирован → Подтвержден" и "Запланирован → Отменен". Добавьте туда пользователей, которые могут подтверждать брони для вашего проекта.

![./pics/Untitled%2010.png](./pics/Untitled%2010.png)

#### Создание типа задачи

![./pics/Untitled%2011.png](./pics/Untitled%2011.png)

Не забудьте нажать "Сохранить" в самом низу страницы

#### Настройка полей очереди

В сайдбаре слева выберите пункт "Поля очереди".

Создайте поле "Проект", тип "Выпадающий список". В значениях списка укажите проект/проекты, по которым вы будете выбирать [конфигурацию из артефакта в Реакторе](#структура-конфига).

![./pics/Untitled%2012.png](./pics/Untitled%2012.png)

**ВАЖНО:** Ключ должен совпадать в точности. Если у вас один проект, достаточно выбрать одно значение. Описание опционально.

Создайте остальные поля как на скриншоте ниже

![./pics/local_fields.png](./pics/local_fields.png)

**ВАЖНО:** Ключ(id) должен совпадать в точности

Для использования регулярной брони создайте поле с типом выпадающий список с ключом: use_regular_booking, значения в списке укажите: "Да", "Нет".

#### Настройка триггеров

В сайдбаре слева выберите пункт "Автоматизация → Триггеры". Создайте триггеры

Вы можете добавить этим триггерам в названии префикс, чтобы было понятно к какому инструменту они относятся

<details><summary><b>Триггер 1: Дожидаться завершения работы предыдущего триггера</b></summary><p>

![./pics/concurrency_trigger.png](./pics/concurrency_trigger.png)

---

</p></details><details><summary><b>Триггер 2: Требовать заполнение обязательных полей</b></summary><p>

![./pics/required_fields_trigger.png](./pics/required_fields_trigger.png)

---

</p></details><details><summary><b>Триггер 3: Забронировать время для тестирования асессорами</b></summary>
<p>

![./pics/book_trigger.png](./pics/book_trigger.png)

**Параметры HTTP запроса**

Адрес: [https://reactor.yandex-team.ru/api/v1/a/i/instantiate/](https://reactor.yandex-team.ru/api/v1/a/i/instantiate/)

Токен: [https://yav.yandex-team.ru/secret/sec-01ex7kr49nhqjxaxhzrpa159e0/explore/version/ver-01ex7kr4a56gb972h19pwaa08j](https://yav.yandex-team.ru/secret/sec-01ex7kr49nhqjxaxhzrpa159e0/explore/version/ver-01ex7kr4a56gb972h19pwaa08j)

Тело запроса (`namespacePath` должен ссылаться на [ваш артефакт](#настройка-реактора))

```json
{
    "artifactIdentifier": {
        "namespaceIdentifier": {
            "namespacePath": "/maps/front/maps/sloth/ВАШ_ПРОЕКТ/create-version-and-book/create-version-and-book_artifact"
        }
    },
    "metadata": {
        "@type": "/yandex.reactor.artifact.StringArtifactValueProto",
        "value": "{{issue.key}}"
    }
}
```

---

</p></details><details><summary><b>Триггер 4: Запустить тестирование асессорами</b></summary><p>

![./pics/launch_trigger.png](./pics/launch_trigger.png)

**Параметры HTTP запроса**

Адрес: [https://reactor.yandex-team.ru/api/v1/a/i/instantiate/](https://reactor.yandex-team.ru/api/v1/a/i/instantiate/)

Токен: [https://yav.yandex-team.ru/secret/sec-01ex7kr49nhqjxaxhzrpa159e0/explore/version/ver-01ex7kr4a56gb972h19pwaa08j](https://yav.yandex-team.ru/secret/sec-01ex7kr49nhqjxaxhzrpa159e0/explore/version/ver-01ex7kr4a56gb972h19pwaa08j)

Тело запроса (`namespacePath` должен ссылаться на [ваш артефакт](#настройка-реактора))

```json
{
    "artifactIdentifier": {
        "namespaceIdentifier": {
            "namespacePath": "/maps/front/maps/sloth/ВАШ_ПРОЕКТ/launch-assessors/launch-assessors_artifact"
        }
    },
    "metadata": {
        "@type": "/yandex.reactor.artifact.StringArtifactValueProto",
        "value": "{{issue.key}}"
    }
}
```

---

</p></details><details><summary><b>Триггер 5: Отменить запуск асессоров</b></summary><p>

![./pics/cancel_trigger.png](./pics/cancel_trigger.png)

**Параметры HTTP запроса**

Адрес: [https://reactor.yandex-team.ru/api/v1/a/i/instantiate/](https://reactor.yandex-team.ru/api/v1/a/i/instantiate/)

Токен: [https://yav.yandex-team.ru/secret/sec-01ex7kr49nhqjxaxhzrpa159e0/explore/version/ver-01ex7kr4a56gb972h19pwaa08j](https://yav.yandex-team.ru/secret/sec-01ex7kr49nhqjxaxhzrpa159e0/explore/version/ver-01ex7kr4a56gb972h19pwaa08j)

Тело запроса (`namespacePath` должен ссылаться на [ваш артефакт](#настройка-реактора))

```json
{
    "artifactIdentifier": {
        "namespaceIdentifier": {
            "namespacePath": "/maps/front/maps/sloth/ВАШ_ПРОЕКТ/cancel-booking/cancel-booking_artifact"
        }
    },
    "metadata": {
        "@type": "/yandex.reactor.artifact.StringArtifactValueProto",
        "value": "{{issue.key}}"
    }
}
```

---

</p></details><details><summary><b>Триггер 6: Обработка ошибок запуска</b></summary><p>

![./pics/error_handling_trigger.png](./pics/error_handling_trigger.png)

---
</p></details><details><summary><b>Триггер 7: Не запускать асессоров при наличии активного запуска</b></summary><p>

![./pics/dupe_hitman_trigger.png](./pics/dupe_hitman_trigger.png)

---

</p></details>

**ВАЖНО:** Настройка триггеров и условий их срабатывания сделана для удобного использования в базовых сценариях работы инструмента, вы можете кастомизировать их работу главными остаются триггеры которые запускают бронирование (3), запускают Хитман процесс(4), отменяют бронирование(5), остальные триггеры выполняют вспомогательные функции блокируя возможность смены статусов или исключая случайные срабатывания основных триггеров. При аналогичной настройке текущих триггеров соблюдайте установленную очередность триггеров в очереди.

#### Синхронизация компонентов

Добавьте компоненты из Testpalm как компоненты трекера в вашу очередь, названия должны совпадать в точности. При этом в TestPalm definition должен именоваться Сomponents. Создание компонентов доступно по ссылке: https://st.yandex-team.ru/НАЗВАНИЕ_ВАШЕЙ_ОЧЕРЕДИ/components

## Использование

### Общий флоу

Взаимодействие с Testpalm, Бронировщиком и Хитманом построено посредством триггеров.

Статус выполнения процесса из триггера указан в поле "Статус согласования". Не переводите статус задачи, пока в поле "Статус согласования" не будет написано "Готов".

Если это все таки произошло, переведите задачу обратно в статус, в котором она была, и дождитесь завершения работы процесса из триггера.

В случае, если **выполнение процесса из триггера завершилось с ошибкой**, в поле "Статус согласования" будет написано "Ошибка". В этом случае, перед дальнейшей работой нужно исправить ошибку, если применимо (например, добавить исполнителя задачи), очистить это поле вручную и перезапустить процесс, нажав на "Перезапустить" в списке статусов задачи.

Инструкции продублированы в комментариях.

#### Работа с тикетом

В общем случае работа с тикетом описывается следующими шагами. В случае кастомизации триггеров/статусов/добавления новых полей она может отличаться, подробности узнавайте у того, кто настраивал вам автоматизацию.

1. Создайте задачу с типом "Тестирование"
2. Укажите исполнителя, [компоненты](#синхронизация-компонентов), [окружение](https://wiki.yandex-team.ru/eva/testing/tech/skills/#desktopnyebrauzery) (Тестирование → Окружение в полях тикета) и QA-инженера (Тестирование → QA-инженер). Если применимо — укажите ссылку на стенд (Тестирование → Ссылка на стенд) и требования для асессоров (Тестирование → Требование для асессоров в полях тикета).
3. Если вам нужен **СРОЧНЫЙ** запуск — повысьте приоритет задачи
4. Укажите ваш [проект](#структура-конфига) в поле Тестирование асессорами → Проект (если этого поля нет в вашем тикете, добавьте его, нажав на кнопку "Выбрать поля" в сайдбаре тикета)
5. Переведите задачу в статус "Запланировать"
6. Затем ответственный QA-инженер будет призван в задачу с просьбой подтвердить вам ваше бронирование
7. QA-инженер проверит правильность заполнения тикета и подтвердит или отклонит бронирование
8. После подтверждения бронирования запустится процесс запуска асессоров
9. После того, как асессоры протестируют вашу задачу, к ней будут прилинкованы найденные баги и в комментариях появится отчет о тестировании.

#### Если вы хотите внести изменения в тикет

Изменения компонентов/окружений, проекта и срочности требуют пересоздания всех сущностей, поэтому нужно начинать все заново.

Для этого нужно отменить задачу. В общем случае — достаточно ее переоткрыть и дождаться, пока сущности удалятся. После этого можете начинать процесс снова.

### Фильтрация кейсов строкой expression
Для фильтрации кейсов можно использовать поле "Фильтр тесткейсов" с id filter_expression. Эту строку можно указывать вручную, заполнять используя макрос, триггер. У этого поля приоритет над остальными, таким образом, если оно не пустое, все условия фильтрации будут браться только из него.

#### Синтаксис
- обращение к definitions: `attributes.my_attribute` или `attributes["my attribute with special characters"]`
- обращение к верхнеуровневым сущностям фильтрации: `status`, `isAutotest`, `createdBy` etc
- простые операторы:
    - `=` или `EQ`
    - `!=` или `NEQ`
    - `>` или `GT` (сравнивают только числа)
    - `<` или `LT` (сравнивают только числа)
    - `~` или `IN` проверка вхождения значения в массив значений
    - `!~` или `NIN` инверсия предыдущего
- сложные операторы:
    - `&` или `AND`
    - `|` или `OR`
- строки всегда заключаются в двойные кавычки
- для значений типа `EMPTY` есть специальное значение `null` (или `NULL`; только для операторов `EQ` и `NEQ`)

### Продвинутая фильтрация по сущностям тестпалма с помощью полей

Для того, чтобы было удобно фильтровать тесткейсы для запуска, можно завести дополнительные локальные поля для очереди. Их также можно будет заполнять макросом, триггером. Поддерживаются только поля с названиями латиницей.

У таких полей нужно задать id, который начинается с `tp__`, например `tp__status`(для всех верхнеуровневых сущностей фильтрации: `status`, `isAutotest`, `createdBy` ). Тип поля на ваше усмотрение: строка (будет разбита в массив по разделителю ","), выпадающий список с одним/несколькими значениями. Для использования "отсутствия" значения есть зарезервированное значение `EMPTY`.

Если хотите добавить возможность фильтрации по `definitions`, создайте поле с id `tp__a_`, например `tp__a_my_testpalm_key`.

Для справки: алгоритм поиска соответствия сущностей из id трекера в фильтрах тестпалма удаляет часть `tp__` или `tp__a_`, затем сравнивает id трекера и поля тестпалма без учета регистра, учитывая только буквы и цифры. Таким образом, нужно избегать применения в проекте ключей, отличающихся лишь регистром и/или спецсимволами.

Например: `tp__a_my_testpalm_key` сматчится на definitions `My testpalm key`, `my testpalm key`, `mytestpalmkey`, `myTestpalmKey!` и т.д. В таком случае не понятно какой именно definition вы имели в виду.

Из выбранных значений в полях фильтрации строится декартово произведение, в котором значения в рамках одного поля объединяются через логическое ИЛИ, а между полями — через логическое И.

Наглядный пример:

В трекере указаны
1) компоненты `behavior`, `ballon`
2) `tp__status` = `actual, draft`
3) `tp__a_my_definition` = `definition1`

Этот тикет распарсится в такую строку фильтра (переносы здесь для удобства):
```
attributes.components = "behavior" & status = "actual" & attributes.my_definition = "definition1" |
attributes.components = "behavior" & status = "draft" & attributes.my_definition = "definition1" |
attributes.components = "balloon" & status = "actual" & attributes.my_definition = "definition1" |
attributes.components = "balloon" & status = "draft" & attributes.my_definition = "definition1" |
```

### Запуск на регулярной брони
Если вы заводили в Трекер поле с ключом use_regular_booking со значениями "Да", "Нет", при конфигурации запуска если вы оставляете поле пустым или ставите "Нет" - будет забронирован слот в обычном режиме, если вы указываете в поле "Да" - запуск идет на регулярной брони указанной Вами в конфиге вашего проекта. 

### Кастомизация

Важно помнить, что sloth это скорее платформа, чем специализированное решение для конкретно ваших воркфлоу и очереди.

Он разработан максимально гибким и опирается на инструментарий тестпалма и трекера, соответственно вы можете вносить любые доработки по оптимизации ваших процессов.

Например, для реализации "пресетов" (предзаполненных значений объединенных некоторым признаком) вы можете воспользоваться макросами трекера.

Для дополнительной автоматизации можно добавить любое локальное поле и установить триггер на его изменение, который будет выполнять любые необходимые вам действия с полями.

Главное, чтобы присутствовали обязательные для запусков поля, которые перечислены в триггере "Требовать заполнение обязательных полей"
