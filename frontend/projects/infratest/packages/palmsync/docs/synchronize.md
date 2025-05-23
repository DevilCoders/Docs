# Синхронизация

Синхронизация выполняет выгрузку тестовых сценариев и данных о авто-тестах в проект в TestPalm.

> :warning: Синхронизация в существующий проект в TestPalm, который существовал до использования palmsync, приведёт к его полному обнулению. Существующие в проекте тест-кейсы будут удалены, а после синхронизации там появятся лишь те тест-кейсы, что написаны в YAML-файлах.

> :book: Инструмент поддерживает синхронизацию одного сервиса в один проект в TestPalm. Если попытаться синхронизировать в проект в TestPalm тест-кейсы из сервиса A, а затем в этот же проект синхронизировать тест-кейсы из сервиса B, то в проекте в TestPalm будут тест-кейсы лишь от последней синхронизации.

Синхронизация выполняется [командой CLI synchronize](./cli.md#palmsync-synchronize), а также может быть выполнена программно при помощи [метода API synchronize](./api.md#synchronize).

Синхронизация происходит следующим образом:

1. выполняется загрузка сценариев проекта из TestPalm;
1. выполняется загрузка сценариев из локальных файлов с описанием и автоматическими тестами;
1. производится сопоставление сценариев из TestPalm и из локальных файлов, после чего происходит одно из действий:
  * сценарии, для которых отсутствуют аналог в проекте в TestPalm, будут добавлены в проект;
  * сценарии, для которых присутствуют аналог в проекте в TestPalm, будут обновлены;
  * сценарии из TestPalm, для которых отсутствуют аналогичные сценарии в локальных файлах, будут удалены из проекта.
1. производится раскрытие [импортированных групп шагов](./steps-group.md).
1. производится [выгрузка скриншотов](./screenshots-upload.md), указанных в кейсах, в S3.

Связь между локальными сценариями и сценариями в TestPalm реализована как соответствие заголовка
сценария в TestPalm и полного имени теста в локальном `*.yml` файле, а так же сопоставляется [тип сценария](./yaml-files.md#Типы-сценариев).

Раскрытие групп шагов по умолчанию отключено, [подробнее](./steps-group.md).
Выгрузка скриншотов в S3-MDS по умолчанию отключена, [подробнее](./screenshots-upload.md).

## Описание сценария в TestPalm

### Заголовок

Полное имя сценария вычисляется как конкатенация (через пробел) 3 составляющих:

1. полей [feature](./yaml-files.md#feature), [type](./yaml-files.md#type) и [experiment](./yaml-files.md#experiment), склеенных через ` / `;
2. всех заголовков тестовых сценариев (suite), склеенных через пробел;
3. заголовка самого теста.
4. Суффикс типа сценария:
  - для [specs-integration](./yaml-files.md#specs-integration) `[integration]`.

Например, для файла ниже полное имя для сценария `Инлайн-установка [manual]` будет `БНО (конструктор) Установка Инлайн-установка [manual]`.

```yaml
feature: БНО (конструктор)

specs:
  beforeEach:
    - do: получить выдачу по запросу 'райффайзенбанк'
    - assert: на выдаче есть сниппет БНО на конструкторе
  Установка:
    Инлайн-установка [manual]:
      - do: кликнуть в последнюю ссылку
      - assert: должна произойти инлайн-установка
```

При наличии полей `type` и `experiment` их значения также участвуют в формировании полного заголовка.

Примеры:

1. При наличии полей `feature` и `type` полное имя для теста `Инлайн-установка [manual]` будет `БНО (конструктор) / Какой-то тип Установка Инлайн-установка [manual]`.

  ```yaml
  feature: БНО (конструктор)
  type: 'Какой-то тип'

  specs:
    Установка:
      Инлайн-установка [manual]:
      ...
  ```

2. При наличии полей `feature` и `experiment` полное имя для теста `Инлайн-установка [manual]` будет `БНО (конструктор) / Какой-то эксперимент Установка Инлайн-установка [manual]`.

  ```yaml
  feature: БНО (конструктор)
  experiment: 'Какой-то эксперимент'

  specs:
    Установка:
      Инлайн-установка [manual]:
      ...
  ```

3. При наличии полей `feature`, `type` и `experiment` полное имя для теста `Инлайн-установка [manual]` будет `БНО (конструктор) / Какой-то тип / Какой-то эксперимент Установка Инлайн-установка [manual]`.

  ```yaml
  feature: БНО (конструктор)
  type: 'Какой-то тип'
  experiment: 'Какой-то эксперимент'

  specs:
    Установка:
      Инлайн-установка [manual]:
      ...
  ```

### Блок описания

При формировании описания сценария используется несколько источников, полученные из них данные располагаются в следующем порядке:

1. ссылка на фильтр в трекере, которая показывает все баги, [привязанные к yaml-файлу](#Привязка-багов-к-yaml-файлам) текущего сценария;
1. описание сценария (поле [description](./yaml-files.md#description) самого сценария);
1. описание из yaml-файла (поле [description](./yaml-files.md#description) в корне);
1. служебная информация сценария (значение шага info);
1. список браузеров с причиной, где сценарий был заскипан в авто-тестах;

### Блок автоматизации

В данном блоке отображается список тикетов в трекере на автоматизацию тест-кейса.
Список тикетов извлекается из ключа сценария [automation](./yaml-files.md#automation).

### Блок предварительных условий

Поле `precondition` в сценариях в TestPalm содержит короткую ссылку на тестируемую среду и соответствующий QR-код.

### Блок с шагами

В данном блоке располагаются [шаги сценария](./yaml-files.md#Шаги-сценария).

Шаги `do`, `assert`, `assertMetrics`, `label` и `tech`, загружаемые из теста, а также из всех хуков `before`, `beforeEach`, `afterEach` и `after` актуальные для данного сценария, преобразуются в список действий.

Шаги `screenshot` выгружаются в описание сценария в виде блока со скриншотами для каждого браузера.

Список шагов, который выгружается в этот блок, в актуальном состоянии, всегда доступен [здесь](https://github.yandex-team.ru/search-interfaces/infratest/blob/master/packages/palmsync/lib/constants/actions.js#L3).

### Блок с ключами

В данный блок выгружаются [поля yaml-файла](./yaml-files.md#Поля-файла).

Список полей указываемых в YAML-файле и подверженных выгрузке:
* [feature](./yaml-files.md#feature) – участвует в формировании заголовка сценария ([подробности](#заголовок)).
* [experiment](./yaml-files.md#experiment) – участвует в формировании заголовка сценария ([подробности](#заголовок)).
* [type](./yaml-files.md#type) – участвует в формировании заголовка сценария ([подробности](#заголовок)).
* [counter](./yaml-files.md#counter) – участвует в формировании свойства `url` сценария ([подробности](#ссылка-на-тестовую-среду-сценария))
* [params](./yaml-files.md#params) – поля `params.*` участвуют в формировании свойства `url` сценария ([подробности](#ссылка-на-тестовую-среду-сценария))
* [browsers](./yaml-files.md#browsers)
* [files](./yaml-files.md#files)
* [langs](./yaml-files.md#langs)
* [manager](./yaml-files.md#manager)
* [priority](./yaml-files.md#priority)
* [qa-engineer](./yaml-files.md#qa-engineer)
* [regions](./yaml-files.md#regions)
* [tlds](./yaml-files.md#tlds)
* [tags](./yaml-files.md#tags) – дополняется значениями по следующим правилам:
  * `not automated` добавляется сценариям, к которым не привязан ни один Hermione-тест (только в случае, если в конфиге указаны [hermioneConfigPath](./configuration.md#hermioneConfigPath) и/или [hermioneE2eConfigPath](./configuration.md#hermioneE2eConfigPath)).
  * `no_assessors` добавляется кейсам, которые не имеют шагов проверки (`assert`, `screenshot`) и имеют хотя бы один `tech`.

Список полей, которые генерируются в процессе синхронизации:
* `skip` — поле, содержащее список браузеров, для которых данный сценарий предназначен, но не запускается из-за заскипа (только в случае, если в конфиге указаны [hermioneConfigPath](./configuration.md#hermioneConfigPath) и/или [hermioneE2eConfigPath](./configuration.md#hermioneE2eConfigPath)). Проставляется, если тесты были заскипаны в коде автотеста или если для hermione включен плагин [external-skip](https://github.yandex-team.ru/search-interfaces/infratest/tree/master/packages/external-skip) или [hermione-muted-tests](https://github.yandex-team.ru/search-interfaces/infratest/blob/master/packages/hermione-muted-tests/package.json). В случае плагина `hermione-muted-tests` мьюты так же будут считаться заскипами.
* `filepath` — относительный путь к `*.yml`-файлу на файловой системе
* `scenarioType` – тип сценария ([подробнее](./yaml-files.md#Типы-сценариев))
* `hermioneTitle` – оригинальный заголовок сценария, который был до применения [testCaseDecorator](./configuration.md#testCaseDecorator).
* `platform` – плафторма, автоматически не проставляется, но желательно это делать самим в [testCaseDecorator](./configuration.md#testCaseDecorator).
* `manual` — добавляется кейсам, в названии которых есть постфикс `[manual]` или присутствует ключ `automation` в теле;

### Блок с расчетным временем

Для каждого сценария считается расчётное время (Estimated time), если в тест-кейсе явно не указано поле `estimatedTime` или автоматический расчёт не отключён.

#### Ручное управление расчётным временем

Каждому тест-кейсу можно задать параметр `estimatedTime` в двух форматах:

1. Число. Время в секундах. Например, `50`.
1. Строка. Время в формате временного интервала (Time Duration / Time Span). Например, `1h10m5s`.

Для временного интервала поддерживаются следующие единицы:

* Секунды (s, sec)
* Минуты (m, min)
* Часы (h, hr)
* Дни (d)

Поддерживается два формата записи временного интервала `1h10m5s` и `1h 10m 5s`.

Пример:

```yaml
specs:
  Заголовок тест-кейса:
    - estimatedTime: 2m 50s
    - do: action
    - assert: expect
```

#### Автоматический расчёт

> 📖 Отключить автоматический расчёт можно используя опцию [`calcEstimatedTime`](./configuration.md#calcEstimatedTime).

Расчётное время рассчитывается следующим образом: берётся число проверочных шагов типа `assert` и `screenshot`, а затем каждое из них умножается на значение стоимости шага, указанное в `assertActionCostInSecs` и `screenshotActionCostInSecs`, соответственно. По умолчанию стоимость любого проверочного шага равна 20 секундам.

Значения для `assertActionCostInSecs` и `screenshotActionCostInSecs` можно установить двумя способами:
* через общую конфигурацию разом для всех тест-кейсов. [Подробнее](./configuration.md#assertActionCostInSecs).
* через [testCaseDecorator](./configuration#testCaseDecorator) отдельно для каждого тест-кейса. Этот способ подходит в тех случаях, когда необходимо установить разные значения для разных платформ.

Пример установки

```js
{
  testCaseDecorator: (testCase) => {
    testCase.setField('assertActionCostInSecs', 40);
    testCase.setField('screenshotActionCostInSecs', 50);
  }
}
```

### Блок со свойствами

#### url

Ссылка на тестовую среду сценария.
При формировании `url` используется следующая логика:

* `host` и `domain` будут взяты из:
  1. [baseUrl](./configuration.md#sets.baseUrl) из конфигурации сета, если есть;
  1. [baseUrl](./configuration.md#baseUrl) из корня конфигурации, если есть;

* `path` будет взят из:
  1. урла, полученного по счётчику из поля `counter`, если счётчик указан и для указанного счётчика есть урл в sandbox-ресурсе [urlsByShowCounters](https://sandbox.yandex-team.ru/tasks?type=URLS_BY_SHOW_COUNTERS&limit=20&created=14_days);
  1. [baseUrl](./configuration.md#sets.baseUrl) из конфигурации сета, если есть;
  1. [baseUrl](./configuration.md#baseUrl) из корня конфигурации, если есть;

* `query`-параметры будут получены при помощи слияния всех `query`-параметров из:
  * ключей из `params.*`;
  * урла по счётчику, если есть;
  * [baseUrl](./configuration.md#sets.baseUrl) из конфигурации сета, если есть;
  * [baseUrl](./configuration.md#baseUrl) из корня конфигурации, если есть;

### Дополнительные свойства

#### flags

Флаги сценария.
Для [specs-honeypots](./yaml-files.md#specs-honeypots) устанавливается флаг `honeypot`. Необходимо для того, чтобы на стороне TestPalm такой сценарий не участвовал в выборках по умолчанию, отображался в соответствии с настройками правил просмотра сценариев (IDM). Подробнее в [FEI-9993](https://st.yandex-team.ru/FEI-9993).

### Привязка багов к yaml-файлам

Тикеты в трекере привязываются к сценариям в TestPalm с помощью свойства в тикете `TestPalm Yaml File`. Где указывается путь к файлу со сценарием относительно корня проекта.

## Ошибки синхронизации

По умолчанию palmsync завершает моментально синхронизацию, если была встречена хотя бы одна ошибка в процессе.
Однако есть ряд ошибок, которые можно смело пропустить, такие ошибки называются "мягкими", актуальный список ошибок всегда доступен [здесь](../lib/synchronizer/errors/index.js). Допустимые кол-во мягких ошибок регулируется с помощью опции [maxSoftErrorsThreshold](./configuration.md#synchronizationOpts). В случае если кол-во мягких ошибок будет превышено допустимое значение, синхронизация завершится с ошибкой.
