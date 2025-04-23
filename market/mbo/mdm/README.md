# Управление мастер-данными - MDM

Кодовая база для новых микросервисов Большого МДМа. "Старый МДМ" расположен в том же репозитории, что и Категорийный Интерфейс: https://a.yandex-team.ru/arc/trunk/arcadia/market/mbo/mbo-category


## Devops

### Дашборды

#### Прод
- [Queue and timings](https://solomon.yandex-team.ru/?project=market-mbo&dashboard=mdm-production)

#### Тестинг
- [Queue and timings](https://solomon.yandex-team.ru/?project=market-mbo&dashboard=mdm-testing)


## Разработка

### Структура проекта:

- MDM Ui `/mdm-ui`

  > Микросервис для раздачи фронта, аутентификации и передачи управления другим компонентам.

- MDM Service API `/mdm-service-api`

  > Микросервис, содержащий сервисы управления данными и метаданными в БМДМ. Служит логической прослойкой между более низкоуровневыми компонентами.

- MDM DQ `/mdm-dqc`

  > Интеграция с third-party системой DQ, куда мы можем делегировать вычисления или где можно производить аналитику по большому массиву данных.

- MDM Metadata `/metadata`

  > Модуль, осуществляющий низкоуровневый доступ к метаданным. Содержит описания атрибутов, типов сущностей в МДМ, способы отображения на страницах и прочие базовые свойства произвольных объектов в системе. НЕ содержит сами объекты.

- MDM Storage `/mdm-storage-api`

  > Микросервис, осуществляющий низкоуровневый доступ к самим данным. НЕ содержит мета-описание сущностей, а только их фактическую начинку.

### Локальный запуск всего сразу

1. Подготовка Mdm Ui.
   - Находим  `ru.yandex.market.mdm.ui.MdmUi`
   - Запускаем треугольником в Idea (неважно, сработает или нет)
   - Идём в Run Configurations и сохраняем этот запуск как новую конфигурацию.
   - Указываем Working Directory `/ваш/путь/до/смонтированной/репы/Arcadia/market/mbo/mdm`
   - Теперь должно запускаться и работать.
2. В точности аналогично для `ru.yandex.market.mdm.metadata.MdmMetadataApplication`.
3. В точности аналогично для `ru.yandex.market.mdm.service.api.MdmServiceApi`.
4. В точности аналогично для `ru.yandex.market.mdm.service.api.MdmStorageApi`.
5. Подготовка фронта.
   - Создаём новую Run-конфигурацию с типом npm.
   - Указываем путь до package.json, например: `..../Arcadia/market/mbo/mdm/mdm-ui/src/frontend/package.json`
   - Command => `start`
   - Снизу в Before Launch добавляем плюсиком _Run External Tool_, как на картинке ![Запуск Ya make перед сборкой фронта](https://jing.yandex-team.ru/files/cloudcat/tool1.png)
   - А потом ещё одну добавляем, как на этой картинке ![Подкладывание дефиниций](https://jing.yandex-team.ru/files/cloudcat/tool2.png)
   - Затем там же в Before Launch добавляем плюсиком _Run npm script_. В нём прописываем Command `ci` и тот же путь до package.json. Порядок запуска этих трёх before-команд важен.
   - Запускаем — должен собраться фронт и открыть дев-страничку на локалхосте.
6. А теперь сделаем запуск этого всего по клику. В Run Configurations создаём новое с типом Compound. Добавляем созданные в пунктах 1-5 конфигурации и готово.

### Релизный пайплайн
https://tsum.yandex-team.ru/pipe/projects/mbo/delivery-dashboard/bmdm

### Запуск микросервиса на дев-сервере
См. инструкцию https://wiki.yandex-team.ru/market/mdm/novichok/#kakrazvernutprilozhenienaaidanadev-okruzhenii

### Локальная отладка аутентификации
По умолчанию в деве мы работаем из-под фейкового юзера с предустановленным набором ролей `test_user`. Чтобы продебажить секьюрити с честными походами через TVM в Blackbox, достаточно сделать два шага:
1. Меняем пропертю `mdm.auth.debug` на false
2. Деплоим приложеньки на aida.market.yandex.net (с локальной машинки не пустит в blackbox)

Приложение, запущенное на дев-сервере можно будет продебажить через ssh-тоннель.

### Построение графа сборки
```
python3 scripts/simplify_ya_dump.py
```

Полученный файл скормить любой graphviz-рисовалке, например https://dreampuf.github.io/GraphvizOnline/
