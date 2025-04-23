# Market Apps CMS Schema
**Build** [![Build status](https://teamcity.yandex-team.ru/app/rest/builds/buildType:(id:Market_AppsMarketCmsSchema_Build)/statusIcon)](https://teamcity.yandex-team.ru/buildConfiguration/Market_AppsMarketCmsSchema_Build?branch=&buildTypeTab=overview&mode=builds)
<br>**Detekt** [![Build status](https://teamcity.yandex-team.ru/app/rest/builds/buildType:(id:Market_AppsMarketCmsSchema_Detekt)/statusIcon)](https://teamcity.yandex-team.ru/buildConfiguration/Market_AppsMarketCmsSchema_Detekt?branch=&buildTypeTab=overview&mode=builds)
<br>**Kotlin Doc** [![Build status](https://teamcity.yandex-team.ru/app/rest/builds/buildType:(id:Market_AppsMarketCmsSchema_GenerateDocumentation)/statusIcon)](https://teamcity.yandex-team.ru/buildConfiguration/Market_AppsMarketCmsSchema_GenerateDocumentation?branch=&buildTypeTab=overview&mode=builds)
<br>**Generation** [![Build status](https://teamcity.yandex-team.ru/app/rest/builds/buildType:(id:Market_AppsMarketCmsSchema_GenerateSchema)/statusIcon)](https://teamcity.yandex-team.ru/buildConfiguration/Market_AppsMarketCmsSchema_GenerateSchema?branch=&buildTypeTab=overview&mode=builds)
<br>**Publication** [![Build status](https://teamcity.yandex-team.ru/app/rest/builds/buildType:(id:Market_AppsMarketCmsSchema_PublishSchema)/statusIcon)](https://teamcity.yandex-team.ru/buildConfiguration/Market_AppsMarketCmsSchema_PublishSchema?branch=&buildTypeTab=overview&mode=builds)

[Чат релизов в Telegram](https://t.me/+54huV2pijGM2YjNi)

[Чат поддержки в Telegram](https://t.me/+z0k978HIe0RhZTFi)

## Настройка проекта

1. Установите и настройте монорепозиторий `arcadia` ([инструкция](https://docs.yandex-team.ru/devtools/intro/quick-start-guide))
2. Установите **Intellij Idea** с [официального сайта](https://www.jetbrains.com/ru-ru/idea/) или через <b>Self Service</b>
3. Запустите **Intellij Idea** и откройте папку с проектом
4. Запустите сборку проекта через кнопку `▶` или комбинацией клавиш `Shift + F10`

## Настройка шаблонов

1. Откройте настройки **Intellij Idea** (Mac OS `⌘ + ,`)
2. Перейдите к настройкам шаблонов (`Editor -> File and Code Templates`)
3. Смените схему шаблонов с `Default` на `Project`

## Правила именования веток

Название ветки должно содержать номер тикета из очереди [MARKETAPPSCMS](https://st.yandex-team.ru/MARKETAPPSCMS) 
и название разрабатываемой фичи. Формат названия `feature/<номер тикета>-<название фичи>`. Пример ветки для тикета https://st.yandex-team.ru/MARKETAPPSCMS-9 `feature/9-read-me`.

## Редактирование схемы

### Как добавить новую Секцию

1. Найдите в дереве проекта папку [namespace/market/mobile/schema/sections](https://a.yandex-team.ru/arcadia/market/cms-kotlin-schema/market-mobile/src/main/kotlin/namespace/market/mobile/schema/sections)
    * Можно использовать подпапки внутри данной директории
2. Нажмите правым кликом на папку, выберите `New -> Cms Section Type`
3. В поле `File name` впишите название новой секции
    * Название секции должно заканчиваться постфиксом `..Section`
    * Название секции должно быть уникальным в рамках неймспейса
4. Добавьте нужные поля в описание секции
    * О том как это сделать читайте в разделе [Как добавить новое поле](#как-добавить-редактируемое-поле)
    
```kotlin
@ExportNode("Моя секция")
val MySection = nodeType {
    extends type Section(SectionParams(resources = ..))
}
```
{% cut "А можно поподробнее?" %}

* Аннотация `@ExportNode` отвечает за добавление секции в схему. 
* Первый параметр `label` отвечает за название типа секции в редакторе материалов. 
* Второй параметр `title` отвечает за фоматирование заголовка секции в редакторе материалов.
* Третий параметр `isAbstract` отвечает за доступность секции для выбора в редакторе (выставите в `true` если эта секция базовая). 
* Расширение типа `Section` необходимо, чтобы секция стала доступна для добавления в список секций.
* Параметр `resources` отвечает за типы ресурсов, с которыми может работать данная секция.
* Если секции не нужен ресурс, можно использовать значение `SectionParams.default`.

{% endcut %}

### Как добавить новый тип Узла
1. Найдите в дереве проекта папку [namespace/market/mobile/schema/nodes](https://a.yandex-team.ru/arcadia/market/cms-kotlin-schema/market-mobile/src/main/kotlin/namespace/market/mobile/schema/nodes)
    * Можно использовать подпапки внутри данной директории
2. Нажмите правым кликом на папку, выберите `New -> Cms Node Type`
3. В поле `File name` впишите название нового узла
4. Добавьте нужные поля в описание типа
    * О том как это сделать читайте в секции [Как добавить новое поле](#как-добавить-редактируемое-поле)

```kotlin
@ExportNode("Мой тип узла")
val MyNode = nodeType {
    
}
```
{% cut "А можно поподробнее?" %}

* Аннотация `@ExportNode` отвечает за добавление узла в схему.
* Первый параметр`label` отвечает за название узла в редакторе материалов.
* Второй параметр `title` отвечает за фоматирование заголовка узла в редакторе материалов.
* Третий параметр `isAbstract` отвечает за доступность узла для выбора в редакторе (выставите в `true` если этот узел базовый).

{% endcut %}

### Как добавить новый тип Материала
1. Найдите в дереве проекта папку [namespace/market/mobile/schema/roots](https://a.yandex-team.ru/arcadia/market/cms-kotlin-schema/market-mobile/src/main/kotlin/namespace/market/mobile/schema/roots)
2. Нажмите правым кликом на папку, выберите `New -> Cms Document Root`
3. В поле `File name` впишите название нового типа материала + `..Root`
4. Добавьте поля, которые должны быть в корне материала
    * О том как это сделать читайте в секции [Как добавить новое поле](#как-добавить-редактируемое-поле)
5. Найдите в дереве проекта папку [namespace/market/mobile/schema/documents](https://a.yandex-team.ru/arcadia/market/cms-kotlin-schema/market-mobile/src/main/kotlin/namespace/market/mobile/schema/documents)
6. Нажмите правым кликом на папку, выберите `New -> Cms Document Type`
7. В поле `File name` впишите название нового типа материала
8. Укажите шаблон ключа для поиска документа

```kotlin
@DocumentRoot
@ExportNode("Мой тип документа")
val MyDocumentRoot = nodeType {
    extends type DocumentRoot
}

@ExportDocument(
    type = "my_document_type",
    editorLabel = "Мой тип документа"
)
val MyDocument = documentType(MyDocumentRoot) {
    template(Dimensions.COMMON_DIMENSIONS)
}
```

{% cut "А можно поподробнее?" %}

* Аннотация `@DocumentRoot` отвечает за добавление полей документа в json.
* Аннотация `@ExportNode` отвечает за добавление узла в схему.
* Первый параметр`label` отвечает за название узла в редакторе материалов.
* Второй параметр `title` отвечает за фоматирование заголовка узла в редакторе материалов.
* Третий параметр `isAbstract` отвечает за доступность узла для выбора в редакторе (выставите в `true` если этот узел базовый).
* Расширение типа `DocumentRoot` обеспечивает экспорт базовых полей документа в json.
* Аннотация `@ExportDocument` отвечает за добавление типа документа в схему.
* Первый параметр `type` отвечате за идентификацию типа документа.
* Второй параметр `editorLabel` отвечает за название документа в редакторе материалов.
* Метод `template(..)` добавляет шаблон ключа для поиска документа.

{% endcut %}

### Как добавить редактируемое поле
Описание редактируемого поля состоит из `названия поля`, `способа редактирования` и `описания значения`.
* В качестве `названия поля` может быть использован любой идентификатор из латинских символов.
* В качестве `способа редактирования` может быть выбран один из доступных редакторов `Editors.*`.
* `Описание значения` задается параметрами выбранного редактора.

```kotlin
@ExportNode("MyType")
val MyType = nodeType {
    "autoplay" editor Editors.booleanAsCheckbox(
        label = "Автопрокрутка",
        defaultValue = false
    )
} 
```

Разные редакторы поддерживают разный набор параметров. Наиболее часто используемые параметры:
* `label` - название поля в редакторе материалов
* `help` - текст подсказки для пользователя (спрятан за иконкой вопроса)
* `valueType` - тип значения при сериализации (`STRING`, `NUMBER`, `BOOLEAN`, `NODE`)
* `editorType` - компонент для редактирования значения (`CHECKBOX`, `LIST_BOX` и т.д.)
* `valueQuantity` - ожидаемое количество значений (`optional`, `single`, `multiple`)
* `defaultValue` - генератор значения по умолчанию
* `allowedTypes` - досупные типы узлов в качестве значения данного поля
* `options` - опции для выбора из выпадающего списка

### Как добавить генерируемое поле
Описание генерируемого поля состоит из `названия поля` и `описания значения`.
* В качестве `названия поля` может быть использован любой идентификатор из латинских символов.
* В качестве `описания значения` может быть использован один из доступных генераторов `Values.*`.

```kotlin
@ExportNode("MyType")
val MyType = nodeType {
    "nodeId" value Values.Generated.BlockId
}
```

Поддержанные генераторы значений:
* `Node` - значение отсутствует
* `Generated` - значение генерируется во время экспорта документа
* `Builtin` - значение определяется во время экспорта схемы
* `Constant` - значение равно заданной константе
* `Auto` - значение генерируется со значениями по умолчанию

## Тестирование схемы

Для того чтобы протестировать новую схему, ее можно опубликовать в отличную от `master` ветку [редактора cms](https://cms.market.yandex.ru). 
1. Выберите в **Intellij Idea** вместо `Generate Schema` конфигурацию `Publish Schema`.

    ![Смена конфигурации](_assets/publish-schema-selection.png =351x140)

2. Запустите публикацию через кнопку `▶` или комбинацией клавиш `Shift + F10`
3. Создайте страницу для тестовой ветки в [редакторе cms](https://cms.market.yandex.ru/editor/documents/create)
    
    ![Создание материала](_assets/create-branch-page.png =798x509)

4. Добавьте связь с `реарр-флагом` чтобы сгенерировался уникальный ключ документа
5. Проверьте на тестовой странице изменения в схеме
6. Удалите тестовую страницу после завершения тестирования

## Как отправить изменения в `master`

1. Запускаем генерацию схемы через кнопку `▶` или комбинацией клавиш `Shift + F10`
2. Если выполнение завершилось ошибкой, исправляем ошибку
    * На схему наложен ряд правил, соблюдение которых проверяется во время генерации схемы и на CI
3. Запускаем статический анализатор через **Terminal** командой `./gradlew detekt`
4. Устанавливаем [плагин](https://docs.yandex-team.ru/devtools/intro/quick-start-guide#ide-plugin-setup) для удобной работы с arcadia
5. Отводим новую ветку от `trunk`

    ![Создание новой ветки](_assets/vcs-create-new-branch-small.png =627x387)

6. Делаем коммит с изменениями в ветку

    ![Коммит изменений](_assets/vcs-commit-changes-small.png =560x400)

7. Пушим изменения в репозиторий

    ![Пуш изменений](_assets/vcs-push-changes-small.png =480x350)

8. Создаем **Pull Request** из новой ветки в `trunk` через интерфейс плагина или [команду в терминале](https://docs.yandex-team.ru/devtools/src/arc/workflow)
   * Название **Pull Request** должно начинаться с ключа тикета
   * Ревьюеры выберутся автоматически, тикет перейдет в статус `Ревью`
   * Если упала проверка правил `detekt`, запустите команду `./gradlew detekt` локально и поправьте замечания
   * Схема автоматически опубликуется в одноименную ветку пространства `market-mobile` [редактора cms](https://cms.market.yandex.ru/editor/schema) (см. [эту джобу в TeamCity](https://teamcity.yandex-team.ru/buildConfiguration/Market_AppsMarketCmsSchema_PublishSchema?mode=builds))
   * Для ветки автоматически сгенерируется `kotlin doc` (см. [эту джобу в TeamCity](https://teamcity.yandex-team.ru/buildConfiguration/Market_AppsMarketCmsSchema_GenerateDocumentation?branch=%3Cdefault%3E&buildTypeTab=overview&mode=builds), артефакт `Artifacts/documentation/index.html`)
9. Дожидаемся завершения всех `required` проверок и код-ревью
   * По окончании ревью тикет перейдет в статус `Решен`
10. Мержим **Pull Request** в `trunk`

Изменения появятся в `master` ветке редактора [https://cms.market.yandex.ru](https://cms.market.yandex.ru) появятся через несколько минут. Следить за этим процессом можно в [телеграм чате](https://t.me/+54huV2pijGM2YjNi). 

## Правила по работе с проектом

* Основной критерий качества схемы это удобство использования в редакторе материалов - **проверяйте ваши изменения в ветке**
* Основная **(protected)** ветка - `trunk`. В нее нельзя коммитить, но можно делать **Pull Request**
* Изменения, относящиеся к схеме, вносятся только в пакет [namespace/market/mobile/schema](https://a.yandex-team.ru/arcadia/market/cms-kotlin-schema/market-mobile)
* Изменения вне пакета [namespace/market/mobile/schema](https://a.yandex-team.ru/arcadia/market/cms-kotlin-schema/market-mobile) нужно согласовывать с [Разработчиками генератора](https://abc.yandex-team.ru/services/developers_of_kotlin_feat_cms/)
* Изменения не должны ломать обратную совместимость для использующихся в проде секций (в будущем будет добавлена автоматическая проверка)
* Устаревшие типы, использующиеся на проде, не удаляются, а помечаются аннотацией `@Deprecated`
* Описание секции не должно содержать параметры верстки на клиенте (например, отступы в `px`/`pt`/`dp` и тд.)

## Команда проекта
* Разработка редактора схемы - [Александр Миронычев](https://staff.yandex-team.ru/aamironychev)
* Разработка основной схемы - [Александр Попсуенко](https://staff.yandex-team.ru/apopsuenko)
* Разработка api редактора - [Роман Червоткин](https://staff.yandex-team.ru/chervotkin)
* UX испытатели - [Александр Попсуенко](https://staff.yandex-team.ru/apopsuenko), [Евгений Мартыненко](https://staff.yandex-team.ru/eugenemartins), [Михаил Смирнов](https://staff.yandex-team.ru/smirnov-mike)

По вопросам поддержки обращайтесь в [телеграм чат](https://t.me/+z0k978HIe0RhZTFi).
