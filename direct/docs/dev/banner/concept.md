# Архитектура баннеров

## Платформа для решения типовых задач { #platform }

Архитектура баннеров — это платформа, которая предоставляет стандартные инструменты для решения типовых бизнес-задач.
Она включает в себя структуру классов и ряд договоренностей.

Примеры типовых задач:

- переиспользование части одного типа баннера в другом типе
- создание нового типа баннера из имеющихся кусочков
- добавление баннерам новых свойств
- управление статусами модерации и синхронизации с БК

Базовая структура классов предоставляет высокую степень гибкости, а договоренности дополняют её таким образом, чтобы похожие бизнес-задачи имели одинаковые по структуре решения. <br/>У такого единообразия есть ряд преимуществ:

- однажды разобравшись в одном кусочке баннера, легко разобраться и в другом
- понятно, куда и как вносить изменения; не нужно заново придумывать то, что уже придумано
- для поиска какого-либо аспекта бизнес-логики достаточно знать название части баннера — из него выводится имя искомого класса

## Ассеты — центральный элемент { #asset }

Центральным элементом архитектуры являются обособленные кусочки баннера — _ассеты_.

Ассеты бывают _простыми_ и _библиотечными_:

- _Простой ассет_ структурно является частью баннера, он не представлен отдельной самостоятельной сущностью. В баннере хранятся непосредственно полезные данные ассета. Примеры: ссылка, отображаемая ссылка ("зеленый URL"), кнопка.

- _Библиотечный ассет_ представлен самостоятельной сущностью, так что разные баннеры могут ссылаться на неё. _Связка баннера с библиотечной сущностью структурно является частью баннера_. И когда мы говорим об ассете в контексте модели баннера (как в данной документации), мы рассматриваем именно связку. Связка содержит идентификатор библиотечной сущности (или несколько в случае отношения один-ко-многим), а так же может содержать дополнительные поля, такие как статус модерации связки. Примеры: картинка, турболендинг, креатив.

Ассеты и _объединения ассетов_ в коде представлены _интерфейсами_ и привязанной к ним бизнес-логикой.

_Конечные типы_ баннеров представлены классами, которые имплементируют интерфейсы. Когда класс баннера имплементирует интерфейс, он получает его поля с данными и всю привязанную к нему бизнес-логику. Так функциональность баннеров собирается из интерфейсов как из кубиков.

Когда говорят "текстовый баннер поддерживает турболендинг", на языке java это выглядит как <br/> `class TextBanner implements BannerWithTurboLanding`.

### Интерфейсы ассетов { #asset-interface }

Каждый ассет представлен в коде интерфейсом, который сам объявляет полезные свойства, а не наследует их от других интерфейсов.
Такой интерфейс называется _базовым_.
Например, интерфейс ассета "турболендинг" — [BannerWithTurboLanding](https://a.yandex-team.ru/arc/trunk/arcadia/direct/libs-internal/core-model/src/generated/java/ru/yandex/direct/core/entity/banner/model/BannerWithTurboLanding.java) — содержит идентификатор турболендинга и его статус модерации.

Есть так же фиксированный список _корневых интерфейсов_:

- [Banner](https://a.yandex-team.ru/arc/trunk/arcadia/direct/libs-internal/core-model/src/generated/java/ru/yandex/direct/core/entity/banner/model/Banner.java) — маркерный интерфейс, лежащий в основе всей иерархии;
- [BannerWithAdGroupId](https://a.yandex-team.ru/arc/trunk/arcadia/direct/libs-internal/core-model/src/generated/java/ru/yandex/direct/core/entity/banner/model/BannerWithAdGroupId.java) — содержит идентификатор группы;
- [BannerWithCampaignId](https://a.yandex-team.ru/arc/trunk/arcadia/direct/libs-internal/core-model/src/generated/java/ru/yandex/direct/core/entity/banner/model/BannerWithCampaignId.java) — содержит идентификатор кампании.

Базовые интерфейсы ассетов могут наследоваться только от корневых.

Если у двух и более ассетов есть общая бизнес-логика (если коду нужно иметь доступ к полям нескольких ассетов),
то они объединяются _агрегирующим интерфейсом_ — таким интерфейсом, который наследуется от нескольких базовых интерфейсов.
Пример: `BannerWithBodyComputedFromCreative extends BannerWithBody, BannerWithCreative`).

У ассета могут быть _дополнительные интерфейсы_ — они наследуются только от одного базового интерфейса и не привносят новых свойств.
Они нужны для отделения части бизнес-логики ассета, если она нужна не в каждом типе баннера, в котором используется ассет.
Пример: `BannerWithFixedBody extends BannerWithBody`.

Таким образом, получается следующая структура интерфейсов:
```text
корневой интерфейс + -> базовый интерфейс A
                   |
                   + -> базовый интерфейс B -> ⎫
                   |                           ⎬-> агрегирующий интерфейс BC
                   + -> базовый интерфейс C -> ⎭
                   |
                   + -> базовый интерфейс D -> дополнительный интерфейс D1
```

{% note info "Обратите внимание" %}

Только базовые интерфейсы могут объявлять новые свойства.
Базовые интерфейсы могут наследоваться только от `Banner`, `BannerWithAdGroupId` и `BannerWithCampaignId`.

{% endnote %}

### Бизнес-логика ассетов — тайп-саппорты { #asset-business-logic }

Интерфейсы ассетов содержат только свойства. Бизнес-логика же сосредоточена в специальных классах, называемых _тайп-саппортами_.

Таким образом, бизнес-логика конечного типа баннера состоит из бизнес-логики тайп-саппортов, подключенных к интерфейсам, которые имплементируются этим конечным типом.

Существует несколько типов тайп-саппортов, отличающихся специализацией:

- _репозиторные_ — отвечают за чтение, добавление и обновление ассета
(имплементируют интерфейс [RepositoryTypeSupport](https://a.yandex-team.ru/arc/trunk/arcadia/direct/libs/multitype/src/main/java/ru/yandex/direct/multitype/repository/RepositoryTypeSupport.java));
могут быть привязаны только к базовым и корневым интерфейсам.
- _валидационные_ — отвечают за валидацию (имплементируют интерфейс
[AddValidationTypeSupport](https://a.yandex-team.ru/arc/trunk/arcadia/direct/libs/multitype/src/main/java/ru/yandex/direct/multitype/service/validation/type/add/AddValidationTypeSupport.java) для операции добавления
или [UpdateValidationTypeSupport](https://a.yandex-team.ru/arc/trunk/arcadia/direct/libs/multitype/src/main/java/ru/yandex/direct/multitype/service/validation/type/update/UpdateValidationTypeSupport.java) для операции обновления)
- _операционные_ — отвечают за управление статусами и дополнительную логику (имплементируют интерфейс
[AddOperationTypeSupport](https://a.yandex-team.ru/arc/trunk/arcadia/direct/libs/multitype/src/main/java/ru/yandex/direct/multitype/service/type/add/AddOperationTypeSupport.java) для операции добавления
или [UpdateOperationTypeSupport](https://a.yandex-team.ru/arc/trunk/arcadia/direct/libs/multitype/src/main/java/ru/yandex/direct/multitype/service/type/update/UpdateOperationTypeSupport.java) для операции обновления).

Тайп-саппорты создаются для интерфейса при необходимости, то есть у интерфейса не обязательно должны быть все возможные тайп-саппорты. В отношениях между интерфейсами и тайп-саппортами существует несколько ограничений:

- каждый тайп-саппорт привязан только к одному интерфейсу;
- у базовых и корневых интерфейсов (кроме маркерного `Banner`) всегда есть репозиторные тайп-саппорты;
- у агрегирующих и дополнительных интерфейсов не может быть репозиторных тайп-саппортов.

Каждый тайп-саппорт работает только в определенном случае. Например, при чтении баннеров из базы используются только репозиторные тайп-саппорты, и только те их методы, которые отвечают за чтение. А если клиент добавляет новый баннер, то в дело вступают все тайп-саппорты, связанные с добавлением.

Формат имен тайп-саппортов: `<имя интерфейса> + <имя тайп-саппорта>`, например `BannerWithButtonRepositoryTypeSupport`.

{% note tip "Поиск в IDE" %}

Строгое соответствие формату именования позволяет быстро находить нужные тайп-саппорты в IDE. Например, чтобы открыть класс `BannerWithButtonRepositoryTypeSupport`, нажмите `SHIFT + SHIFT`, а затем в открывшемся окне введите `NBWBRTS`.

{% endnote %}

### Расположение ассетов { #asset-directory }

Каждый ассет имеет собственную директорию в [core/entity/banner/type](https://a.yandex-team.ru/arc/trunk/arcadia/direct/core/src/main/java/ru/yandex/direct/core/entity/banner/type). В ней расположены все его тайп-саппорты, как точки входа в бизнес-логику, а так же вспомогательные классы. Например, директория ассета "кнопка": [banner/type/button](https://a.yandex-team.ru/arc/trunk/arcadia/direct/core/src/main/java/ru/yandex/direct/core/entity/banner/type/button).

{% note info "Расположение объединений ассетов" %}

Объединения ассетов не имеют собственных директорий. Тайп-саппорты для агрегирующего интерфейса располагаются в директории одного из входящих в его состав ассетов.

{% endnote %}

### Генерация классов и интерфейсов { #asset-model-gen }

Все интерфейсы и конечные классы генерируются с помощью инструмента [model-generator](https://a.yandex-team.ru/arc/trunk/arcadia/direct/libs/model-generator) из конфигурационных файлов, расположенных в директории [model-conf/banner](https://a.yandex-team.ru/arc/trunk/arcadia/direct/libs-internal/core-model/src/main/model-conf/banner).

Формат имён файлов базовых интерфейсов: `i_banner_with_ + <имя ассета>`.<br/>
Пример: [i_banner_with_body.conf](https://a.yandex-team.ru/arc/trunk/arcadia/direct/libs-internal/core-model/src/main/model-conf/banner/i_banner_with_body.conf)

Формат имён файлов агрегирующих интерфейсов: `i_banner_with_ + <описание объединения>`.<br/>
Лучше всего, когда удается дать имя по существу: [i_banner_with_body_computed_from_creative.conf](https://a.yandex-team.ru/arc/trunk/arcadia/direct/libs-internal/core-model/src/main/model-conf/banner/i_banner_with_body_computed_from_creative.conf). <br/>
Но обычно имя состоит из перечисления ассетов: [i_banner_with_href_and_display_href.conf](https://a.yandex-team.ru/arc/trunk/arcadia/direct/libs-internal/core-model/src/main/model-conf/banner/i_banner_with_href_and_display_href.conf).

Формат имён файлов конечных типов баннеров: `class_ + <тип баннера>`.<br/>
Пример: [class_cpc_video.conf](https://a.yandex-team.ru/arc/trunk/arcadia/direct/libs-internal/core-model/src/main/model-conf/banner/class_cpc_video.conf).

{% note info %}

Конфигурационные файлы дополнительных классов, которые не входят в иерархию ассетов лучше записывать без префиксов `i_` и `class_`.

{% endnote %}

{% note info %}

Конфигурационные файлы для смежных областей вроде транспортов в БК и Модерацию рекомендуется складывать в поддиректории, как это [сделано](https://a.yandex-team.ru/arc/trunk/arcadia/direct/libs-internal/core-model/src/main/model-conf/banner/bsexport) для транспорта в БК.

{% endnote %}

## Ключевые отличия от архитектуры кампаний

### Отличия в применении интерфейсов

Баннеры и кампании реализованы на базе одного [фреймворка](https://a.yandex-team.ru/arc/trunk/arcadia/direct/libs/multitype/src/main/java/ru/yandex/direct/multitype), но между ними есть ряд важных отличий.

В кампаниях интерфейсы применяются для выделения любого кусочка логики, который присутствует в одном конечном типе и отсутствует в другом.
По сути логика конечного типа кампании определяется декларативно — списком её интерфейсов.
У такой крайней степени применения интерфейсов есть несколько недостатков:

- логика разбросана по большому числу интерфейсов, сложно понять что получается в сумме, сложно поддерживать код в оптимальном состоянии;
- интерфейсы часто приходится разделять на несколько других интерфейсов — это сложночитаемые и рискованные изменения.

В баннерах используется более умеренный, гибридный подход.
В основном используются только базовые интерфейсы ассетов и агрегирующие интерфейсы для их объединения.
Для переопределения дефолтной логики ассета используются конструкции if-return.
Отчасти это сделано для простоты управления интерфейсами баннера, а отчасти потому что логика баннеров зависит не только от его типа, но и от типа группы и кампании, а так же от их настроек и включенности фич, поэтому в общем случае декларативный подход не применим.
Дополнительные интерфейсы с отдельной логикой тоже применяются, но редко — когда есть очень обособленная, исключительная логика, не фигурирующая в корневом интерфейсе.

### Отличия в расположении классов

В кампаниях тайп-саппорты сгруппированы по назначению.
Например, в [campaign/repository/type](https://a.yandex-team.ru/arc/trunk/arcadia/direct/core/src/main/java/ru/yandex/direct/core/entity/campaign/repository/type) находятся все репозиторные тайп-саппорты,
а в [campaign/service/type/add](https://a.yandex-team.ru/arc/trunk/arcadia/direct/core/src/main/java/ru/yandex/direct/core/entity/campaign/service/type/add) — все операционные тайп-саппорты операции добавления.

В баннерах центральным элементом является ассет. Поэтому, все тайп-саппорты одного ассета находятся в одной директории. Таким образом, вся логика одного ассета находится в одном месте. Пример: [banner/type/button](https://a.yandex-team.ru/arc/trunk/arcadia/direct/core/src/main/java/ru/yandex/direct/core/entity/banner/type/button).

Все тайп-саппорты агрегирующего интерфейса находятся в одной из директорий его базовых интерфейсов.

Общие для нескольких тайп-саппортов классы находятся на верхнем уровне: в [entity/banner/service](https://a.yandex-team.ru/arc/trunk/arcadia/direct/core/src/main/java/ru/yandex/direct/core/entity/banner/service) и [entity/banner/repository](https://a.yandex-team.ru/arc/trunk/arcadia/direct/core/src/main/java/ru/yandex/direct/core/entity/banner/repository). Например, [banner/service/text/CompoundTextExtractor](https://a.yandex-team.ru/arc/trunk/arcadia/direct/core/src/main/java/ru/yandex/direct/core/entity/banner/service/text/CompoundTextExtractor.java) извлекает текст из любого типа баннера в зависимости от того, какие интерфейсы он реализует.

## Репозитории { #repo }

В баннерах репозитории делятся по темам или по назначению:

- [BannerTypedRepository](https://a.yandex-team.ru/arc/trunk/arcadia/direct/core/src/main/java/ru/yandex/direct/core/entity/banner/repository/BannerTypedRepository.java) — для чтения целых классов и интерфейсов баннеров, с любыми условиями выборки;
- [BannerModifyRepository](https://a.yandex-team.ru/arc/trunk/arcadia/direct/core/src/main/java/ru/yandex/direct/core/entity/banner/repository/BannerModifyRepository.java) — для добавления/обновления баннеров;
- [BannerRelationsRepository](https://a.yandex-team.ru/arc/trunk/arcadia/direct/core/src/main/java/ru/yandex/direct/core/entity/banner/repository/BannerRelationsRepository.java) — для извлечения идентификаторов, например мапы id группы по id баннеров;
- [BannerModerationRepository](https://a.yandex-team.ru/arc/trunk/arcadia/direct/core/src/main/java/ru/yandex/direct/core/entity/banner/repository/BannerModerationRepository.java) — для запросов, специфических для модерации;
- [BannerCommonRepository](https://a.yandex-team.ru/arc/trunk/arcadia/direct/core/src/main/java/ru/yandex/direct/core/entity/banner/repository/BannerCommonRepository.java) — для всего, что сложно отнести к одному из тематических репозиториев.

{% note tip %}

При необходимости добавляйте собственный тематические репозитории. Старайтесь избегать создания бога-репозитория с большим числом разношерстных методов.

{% endnote %}

### Чтение { #repo-read }

Чтение классов и интерфейсов баннеров осуществляется посредством репозитория [BannerTypedRepository](https://a.yandex-team.ru/arc/trunk/arcadia/direct/core/src/main/java/ru/yandex/direct/core/entity/banner/repository/BannerTypedRepository.java), который наследуется от более универсального [TypedRepository](https://a.yandex-team.ru/arc/trunk/arcadia/direct/libs/multitype/src/main/java/ru/yandex/direct/multitype/repository/TypedRepository.java).

Баннеры извлекаются из БД в два этапа:

1. Запрос за данными из таблицы [banners](https://direct-dev.yandex-team.ru/db/ppc/tables/banners.html) и тех таблиц, которые имеют с ней отношение один-к-одному. Для построения запроса репозиторий получает у тайп-саппортов список полей БД (`RepositoryTypeSupport.getFields`), а так же делегирует им джойн необходимых таблиц (`RepositoryTypeSupport.addSelectJoin`). Когда данные извлечены из базы, тайп-саппорты заполняют модели баннеров (`RepositoryTypeSupport.fillFromRecord`).
1. Запросы за данными из таблиц, которые имеют отношение один-ко-многим с таблицой [banners](https://direct-dev.yandex-team.ru/db/ppc/tables/banners.html). Этот этап полностью делегируется тайп-саппортам (`RepositoryTypeSupport.enrichModelFromOtherTables`).

Существует ряд методов для извлечения баннеров или отдельных их частей из базы, они делятся на несколько групп.

#### Методы getTyped { #repo-read-typed }

Методы `getTyped*` выбирают из базы полностью заполненные баннеры. Ключевой их особенностью является то, что в момент вызова они ничего не знают о типах запрашиваемых баннеров. Как следствие, на первом этапе выборки джойнятся все таблицы баннеров и запрашиваются все поля. На втором этапе типы баннеров уже известны, а следовательно известны и соответствующие им тайп-саппорты, поэтому делаются только необходимые запросы в базу (подробнее в разделе [Чтение](#repo-read)).

Эти методы используются, если нужно выбрать полностью заполненные баннеры.

```java
// создаем два баннера: TextBanner и CpcVideoBanner
List<Long> ids = bannerModifyRepository.add(context, container,
        asList(textBanner, cpcVideoBanner));

// получаем баннеры методом getTyped
List<Banner> banners = bannerTypedRepository.getTyped(shard, ids);

// проверяем результат
System.out.println("count: " + banners.size());
banners.forEach(banner -> System.out.println("class: " + banner.getClass()));
```
Вывод:
```text
count: 2
class: class ru.yandex.direct.core.entity.banner.model.TextBanner
class: class ru.yandex.direct.core.entity.banner.model.CpcVideoBanner
```

#### Методы getSafely { #repo-read-safely }

Методы `getSafely*` принимают в качестве аргумента требуемый тип.
В качестве типа может выступать любой интерфейс или конечный тип баннера.
Эти методы выбирают из базы только те данные, которые необходимы для заполнения полей указанного типа.
Если в выборку попали баннеры, не соответствующие указанному типу, то они отбрасываются (поэтому — "safely").

Эти методы используются, если:

- нужно выбрать только баннеры определенного типа (в т.ч. имплементирующие определенный интерфейс), а остальные проигнорировать;
- нужны только данные указанного интерфейса или класса.

##### getSafely для списка интерфейсов { #repo-read-safely-for-collection-of-interfaces }

Есть версия метода getSafely принимающая коллекцию интерфейсов. Заполняются поля всех переданных интерфейсов, а в выборку попадают баннеры имплементирующие хотя бы один из интерфейсов (т.е. интерфейсы в списке идут через "или").

{% note tip "Выборка нескольких интерфейсов (через 'и') одним запросом" %}

Если вы хотите за один запрос в базу получить объекты имплементирующие одновременно несколько интерфейсов, заведите агрегирующий интерфейс (подробнее в разделе [Интерфейсы ассетов](#asset-interface)).

{% endnote %}

```java
System.out.println("textBanner instanceof BannerWithPrice == " +
        (textBanner instanceof BannerWithPrice));
System.out.println("cpcVideoBanner instanceof BannerWithPrice == " +
        (cpcVideoBanner instanceof BannerWithPrice));

// создаем два баннера: TextBanner и CpcVideoBanner
List<Long> ids = bannerModifyRepository.add(context, container,
        asList(textBanner, cpcVideoBanner));

// получаем баннеры методом getSafely
List<BannerWithPrice> banners =
        bannerTypedRepository.getSafely(shard, ids, BannerWithPrice.class);

// проверяем результат
System.out.println("count: " + banners.size());
banners.forEach(banner -> System.out.println("class: " + banner.getClass()));
```
Вывод:
```text
textBanner instanceof BannerWithPrice == true
cpcVideoBanner instanceof BannerWithPrice == false
count: 1
class: class ru.yandex.direct.core.entity.banner.model.TextBanner
```

#### Методы getStrictly { #repo-read-strictly }

Методы `getStrictly*` принимают в качестве аргумента требуемый тип, и по механизму извлечения данных аналогичны методам [getSafely](#repo-read-safely). Отличие состоит в том, что если в выборку попадает баннер, который не имплементирует указанный тип, то генерируется исключение.

Эти методы используются, если:

- на этапе выборки требуется гарантия, что все баннеры принадлежат указанному типу и будут извлечены из базы;
- нужны только данные указанного интерфейса или класса.

#### Методы getStrictlyFullyFilled { #repo-read-strictly-full }

Методы `getStrictlyFullyFilled*` принимают в качестве аргумента требуемый тип, и по механизму извлечения данных аналогичны методам [getTyped](#repo-read-typed). Они возвращают полностью заполненные объекты. Отличие состоит в том, что если в выборку попадает баннер, который не имплементирует указанный тип, то генерируется исключение.

Эти методы используются, если:

- на этапе выборки требуется гарантия, что все баннеры принадлежат указанному типу и будут извлечены из базы;
- нужны не только данные указанного интерфейса, а полностью заполненные конечные типы.

#### Реализация чтения ассета { #repo-read-impl }

При чтении баннеров из базы [TypedRepository](https://a.yandex-team.ru/arc/trunk/arcadia/direct/libs/multitype/src/main/java/ru/yandex/direct/multitype/repository/TypedRepository.java) делегирует тайп-саппортам специфичную для отдельных ассетов логику. Тайп-саппорты должны имплементировать следующие методы интерфейса [RepositoryTypeSupport](https://a.yandex-team.ru/arc/trunk/arcadia/direct/libs/multitype/src/main/java/ru/yandex/direct/multitype/repository/RepositoryTypeSupport.java):

- `addSelectJoin` (пример: [AbstractRelatedEntityUpsertRepositoryTypeSupport](https://a.yandex-team.ru/arc/trunk/arcadia/direct/core/src/main/java/ru/yandex/direct/core/entity/banner/repository/type/AbstractRelatedEntityUpsertRepositoryTypeSupport.java))
- `getFields` (пример: [AbstractFlatRelatedEntityUpsertRepositoryTypeSupport](https://a.yandex-team.ru/arc/trunk/arcadia/direct/core/src/main/java/ru/yandex/direct/core/entity/banner/repository/type/AbstractFlatRelatedEntityUpsertRepositoryTypeSupport.java))
- `fillFromRecord` (пример: [AbstractFlatRelatedEntityUpsertRepositoryTypeSupport](https://a.yandex-team.ru/arc/trunk/arcadia/direct/core/src/main/java/ru/yandex/direct/core/entity/banner/repository/type/AbstractFlatRelatedEntityUpsertRepositoryTypeSupport.java))
- `enrichModelFromOtherTables` (пример: [BannerWithCalloutsRepositoryTypeSupport](https://a.yandex-team.ru/arc/trunk/arcadia/direct/core/src/main/java/ru/yandex/direct/core/entity/banner/type/callouts/BannerWithCalloutsRepositoryTypeSupport.java))

Подробную информацию о методах читайте в [javadoc](https://a.yandex-team.ru/arc/trunk/arcadia/direct/libs/multitype/src/main/java/ru/yandex/direct/multitype/repository/RepositoryTypeSupport.java).

{% note info %}

Для реализации репозиторных тайп-саппортов рекомендуется использовать абстрактные тайп-саппорты. Подробнее в разделе [Удобные абстрактные репозиторные тайп-саппорты](#repo-convenient).

{% endnote %}

### Создание { #repo-add }

Создание баннеров осуществляется посредством репозитория [BannerModifyRepository](https://a.yandex-team.ru/arc/trunk/arcadia/direct/core/src/main/java/ru/yandex/direct/core/entity/banner/repository/BannerModifyRepository.java), который наследуется от более универсального [TypeModifyRepository](https://a.yandex-team.ru/arc/trunk/arcadia/direct/libs/multitype/src/main/java/ru/yandex/direct/multitype/repository/TypeModifyRepository.java).

Баннеры создаются в БД в три этапа:

1. Генерируются идентификаторы баннеров и проставляются в модели.
1. Из релевантных тайп-саппортов собираются данные для вставки в основную таблицу [banners](https://direct-dev.yandex-team.ru/db/ppc/tables/banners.html) (`RepositoryTypeSupport.pushToInsert`), после чего репозиторий выполняет insert.
1. У релевантных тайп-саппортов вызывается метод для самостоятельной вставки данных в дополнительные таблицы (`RepositoryTypeSupport.insertToAdditionTables`).

Таким образом, в репозиторном тайп-саппорте должен быть реализован строго один из двух методов интерфейса [RepositoryTypeSupport](https://a.yandex-team.ru/arc/trunk/arcadia/direct/libs/multitype/src/main/java/ru/yandex/direct/multitype/repository/RepositoryTypeSupport.java): `pushToInsert` или `insertToAdditionTables`. За подробной информацией обращайтесь к javadoc.

{% note info %}

Для реализации репозиторных тайп-саппортов рекомендуется использовать абстрактные тайп-саппорты. Подробнее в разделе [Удобные абстрактные репозиторные тайп-саппорты](#repo-convenient).

{% endnote %}

### Обновление { #repo-update }

Обновление баннеров осуществляется посредством репозитория [BannerModifyRepository](https://a.yandex-team.ru/arc/trunk/arcadia/direct/core/src/main/java/ru/yandex/direct/core/entity/banner/repository/BannerModifyRepository.java), который наследуется от более универсального [TypeModifyRepository](https://a.yandex-team.ru/arc/trunk/arcadia/direct/libs/multitype/src/main/java/ru/yandex/direct/multitype/repository/TypeModifyRepository.java).

Баннеры обновляются в БД в три этапа:

1. Залочивается основная таблица [banners](https://direct-dev.yandex-team.ru/db/ppc/tables/banners.html) и все дополнительные таблицы в отношении один-к-одному с помощью sql-запроса `select ... for update`. Для джойна таблиц у _всех_ тайп-саппортов вызывается метод `RepositoryTypeSupport.addSelectJoin` (не только у релевантных обновляемым типам баннеров).
1. Из релевантных тайп-саппортов собираются данные для обновления в основной таблице [banners](https://direct-dev.yandex-team.ru/db/ppc/tables/banners.html) (`RepositoryTypeSupport.processUpdate`), после чего репозиторий выполняет update.
1. У релевантных тайп-саппортов вызываются методы для самостоятельного обновления данных в дополнительных таблицах  (`RepositoryTypeSupport.updateAdditionTables`).

Таким образом, в репозиторном тайп-саппорте должен быть реализован строго один из двух методов интерфейса [RepositoryTypeSupport](https://a.yandex-team.ru/arc/trunk/arcadia/direct/libs/multitype/src/main/java/ru/yandex/direct/multitype/repository/RepositoryTypeSupport.java): `processUpdate` или `updateAdditionTables`. За подробной информацией обращайтесь к javadoc.

{% note info %}

Для реализации репозиторных тайп-саппортов рекомендуется использовать абстрактные тайп-саппорты. Подробнее в разделе [Удобные абстрактные репозиторные тайп-саппорты](#repo-convenient).

{% endnote %}

{% note info %}

Кроме непосредственно обновления моделей в транзакции так же выполняется и другая работа. Подробности смотрите в методе [BannersUpdateOperation.execute](https://a.yandex-team.ru/arc/trunk/arcadia/direct/core/src/main/java/ru/yandex/direct/core/entity/banner/service/BannersUpdateOperation.java).

{% endnote %}

### Удобные абстрактные репозиторные тайп-саппорты { #repo-convenient }

Для реализации конечных _тайп-саппортов_ существуют удобные абстрактные классы.
Они реализуют часть полезной логики и предоставляют упрощенный интерфейс.
Более подробная информация по каждому классу есть в javadoc, а примеры использования — в продакшеновом коде.

Для основной таблицы [banners](https://direct-dev.yandex-team.ru/db/ppc/tables/banners.html):

- [AbstractBannerDefaultRepositoryTypeSupport](https://a.yandex-team.ru/arc/trunk/arcadia/direct/core/src/main/java/ru/yandex/direct/core/entity/banner/repository/type/AbstractBannerDefaultRepositoryTypeSupport.java)

Для дополнительных таблиц в соотношении один-к-одному:

- [AbstractFlatRelatedEntityUpsertRepositoryTypeSupport](https://a.yandex-team.ru/arc/trunk/arcadia/direct/core/src/main/java/ru/yandex/direct/core/entity/banner/repository/type/AbstractFlatRelatedEntityUpsertRepositoryTypeSupport.java)
- [AbstractFlatRelatedEntityRepositoryTypeSupport](https://a.yandex-team.ru/arc/trunk/arcadia/direct/core/src/main/java/ru/yandex/direct/core/entity/banner/repository/type/AbstractFlatRelatedEntityRepositoryTypeSupport.java)
- [AbstractNestedRelatedEntityUpsertRepositoryTypeSupport](https://a.yandex-team.ru/arc/trunk/arcadia/direct/core/src/main/java/ru/yandex/direct/core/entity/banner/repository/type/AbstractNestedRelatedEntityUpsertRepositoryTypeSupport.java)
- [AbstractRelatedSingleFieldRepositoryTypeSupport](https://a.yandex-team.ru/arc/trunk/arcadia/direct/core/src/main/java/ru/yandex/direct/core/entity/banner/repository/type/AbstractRelatedSingleFieldRepositoryTypeSupport.java)

Для дополнительных таблиц в соотношении один-ко-многим:

- [AbstractMultiRowEntityRepositoryTypeSupport](https://a.yandex-team.ru/arc/trunk/arcadia/direct/core/src/main/java/ru/yandex/direct/core/entity/banner/repository/type/AbstractMultiRowEntityRepositoryTypeSupport.java)

## Операция добавления { #op-add }

Код: [BannersAddOperation](https://a.yandex-team.ru/arc/trunk/arcadia/direct/core/src/main/java/ru/yandex/direct/core/entity/banner/service/BannersAddOperation.java).

Что делает операция:

- в несколько этапов проводит валидацию, делегируя конкретные проверки валидационным тайп-саппортам;
- в несколько этапов выполняет дополнительные действия, делегируя это операционным тайп-саппортам;
- сохраняет валидные баннеры, делегируя это репозиторию, который в свою очередь делегирует это репозиторным тайп-саппортам.

Особенности:

- работа с баннерами только одного клиента
- бизнес-логика рассчитана на то, что операция выполняется пользователем, а не системой
- работа от имени "оператора" — того, кто непосредственно делает запрос через внешний интерфейс (API, Web)

{% note warning "Проверка фич" %}

Для проверки доступности фич необходимо использовать список фич из контейнера (подробнее в разделе [Контейнеры](#container)), а не обращаться напрямую в `FeatureService`. Так гарантируется фиксированное состояние фич во всех частях операции.

{% endnote %}

### Воркфлоу операции добавления { #op-add-workflow }

Выполнение операции состоит из двух частей:

- подготовка, которая включает в себя валидацию (`AbstractAddOperation.prepare`);
- непосредственно применение изменений (`AbstractAddOperation.apply`).

#### Подготовка { #op-add-workflow-prepare }

На этапе подготовки в определенном порядке вызываются методы валидационных и операционных тайп-саппортов
(подробнее о типах тайп-саппортов в разделе [Бизнес-логика ассетов — тайп-саппорты](#asset-business-logic)).

{% note warning "На этапе подготовки не допускается изменение состояния БД" %}

Контракт операций декларирует, что изменения в базе данных производятся только на этапе применения изменений. Клиентский код может выполнить этап подготовки для получения результата валидации и при этом рассчитывать на то, что это не приведет к каким-либо изменениям в БД.

{% endnote %}

Подготовка состоит из следующих этапов:

1. _Заполнение контейнеров._ Подробнее в разделе [Контейнеры](#container).

1. _Превалидация._ У валидационных тайп-саппортов вызывается метод `AddValidationTypeSupport.preValidate`. Этот этап используется в исключительных случаях, например, для проверки прав на добавление баннеров в указанную группу, чтобы отсечь неудовлетворяющие этой проверке баннеры на самом раннем этапе.

1. _Действия после превалидации._ Успешно прошедшие превалидацию баннеры передаются операционным тайп-саппортам в метод `AddOperationTypeSupport.onPreValidated`. В этом методе над ними можно выполнять любую работу, например вычислять значения полей.

1. _Основная валидация._ У валидационных тайп-саппортов вызывается метод `AddValidationTypeSupport.validate`, куда передается результат превалидации всех баннеров, в том числе с ошибками превалидации.

1. _Действия после основной валидации._ Успешно прошедшие оба этапа валидации баннеры передаются в метод `AddOperationTypeSupport.onModelsValidated`. Это первый этап, когда баннеры можно считать валидными. В этом методе может быть выполнена любая дополнительная работа по подготовке баннеров к сохранению, в том числе их модификация.

{% note info "На этапе подготовки вызываются тайп-саппорты разных типов" %}

На этапе подготовки последовательно вызываются методы разных тайп-саппортов: `AddValidationTypeSupport` и `AddOperationTypeSupport`. В операционный тайп-саппорт передаются только объекты, успешно прошедшие все предшествующие этапы валидации. При этом порядок обращения к конкретным тайп-саппортам не определен.

{% endnote %}

{% note warning "В валидационных тайп-саппортах не допускается изменение объектов баннеров" %}

Такая договоренность необходима для четкого разделения обязанностей между тайп-саппортами. Её соблюдение облегчает поддержку и развитие продукта.

{% endnote %}

{% note tip "На каком этапе лучше делать валидацию?" %}

По умолчанию вся валидация проводится на основном этапе — в методе `AddValidationTypeSupport.validate`.
Превалидация используется в экзотических случаях.
Например, если нужно выполнить часть валидации, затем как-то преобразовать модель, затем выполнить еще часть валидации.
Или, для симметрии с операцией обновления (в операции обновления у превалидации другое назначение).

{% endnote %}

#### Применение изменений { #op-add-workflow-apply }

{% note info "Условие применения изменений" %}

Описываемые здесь этапы выполняются только в том случае, если валидация прошла успешно с учетом режима работы операции. В режиме `PARTIAL` нужен минимум один валидный объект. Режим `FULL` требует, чтобы все объекты были валидны. Если применение изменений невозможно, то ни один из последующих этапов не будет выполнен.

{% endnote %}

Применение изменений состоит из следующих этапов:

1. _Действия перед сохранением баннеров вне транзакции._ У операционных тайп-саппортов вызывается метод `AddOperationTypeSupport.beforeExecution`. Этот метод чаще всего используется для изменения значений полей перед сохранением (например, статусов модерации ассета: [BannerWithButtonAddOperationTypeSupport](https://a.yandex-team.ru/arc/trunk/arcadia/direct/core/src/main/java/ru/yandex/direct/core/entity/banner/type/button/BannerWithButtonAddOperationTypeSupport.java)).

1. _Добавление информации в контейнер дополнительных действий_. У операционных тайп-саппортов вызывается метод `AddOperationTypeSupport.addToAdditionalActionsContainer`, в котором они могут добавить идентификаторы объектов в контейнер дополнительных действий (подробнее в разделе [Контейнер дополнительных действий и его сервис](#container-additional-actions)).

1. _Создание баннеров в базе_. Открывается транзакция и вызывается соответствующий метод репозитория (подробнее о работе репозитория в разделе [Создание](#repo-add)).

1. _Дополнительные действия в транзакции._ У операционных тайп-саппортов вызывается метод `AddOperationTypeSupport.updateRelatedEntitiesInTransaction`, куда передается контекст открытой на предыдущем шаге транзакции `DSLContext dslContext`.

1. _Обработка контейнера дополнительных действий._ Сервис [BannerAdditionalActionsService](https://a.yandex-team.ru/arc/trunk/arcadia/direct/core/src/main/java/ru/yandex/direct/core/entity/banner/service/BannerAdditionalActionsService.java) выполняет дополнительные действия над объектами, добавленными в контейнер на втором шаге.

{% note info "На этапе применения изменений допускается изменение состояния баннеров" %}

Этап применения изменений подразумевает как сохранение моделей в базу данных, так и их предварительную обработку.

{% endnote %}

### Статусы модерации баннера в операции добавления { #op-add-banner-moderation }

При добавлении статусы модерации баннера не зависят от содержимого, а только от статусов модерации родительских объектов: группы и кампании.

Статусы модерации баннера выделены в отдельный ассет — интерфейс `BannerWithModerationStatuses`.
Они вычисляются в [BannerWithModerationStatusesAddOperationTypeSupport](https://a.yandex-team.ru/arc/trunk/arcadia/direct/core/src/main/java/ru/yandex/direct/core/entity/banner/type/moderation/BannerWithModerationStatusesAddOperationTypeSupport.java).

Тайп-саппорт делегирует вычисление статусов и выполнение дополнительных действий со смежными объектами специальным процессорам в зависимости от конечного типа баннера. Дефолтный процессор [DefaultAddOperationModerationProcessor](https://a.yandex-team.ru/arc/trunk/arcadia/direct/core/src/main/java/ru/yandex/direct/core/entity/banner/type/moderation/DefaultAddOperationModerationProcessor.java) реализует стандартную логику вычисления статусов и срабатывает для тех типов баннеров, для которых не зарегистрирован специфичный процессор. Специфичные процессоры нужны для того, чтобы переопределить стандартную логику, например чтобы включить автоприемку на стороне Директа и не отправлять баннер в Модерацию.

Процессоры регистрируются в тайп-саппорте с помощью Spring-фреймворка.
Чтобы переопределить логику для определенного типа баннера, достаточно добавить класс процессора в директорию [banner/type/moderation](https://a.yandex-team.ru/arc/trunk/arcadia/direct/core/src/main/java/ru/yandex/direct/core/entity/banner/type/moderation)
и пометить его аннотацией `@Component` — он автоматически подключится в [BannerWithModerationStatusesAddOperationTypeSupport](https://a.yandex-team.ru/arc/trunk/arcadia/direct/core/src/main/java/ru/yandex/direct/core/entity/banner/type/moderation/BannerWithModerationStatusesAddOperationTypeSupport.java).
Чтобы затем выключить специфическую логику модерации для этого типа баннера, достаточно удалить процессор из кода, и тогда будет срабатывать стандартная логика.

### Статус модерации ассета в операции добавления { #op-add-asset-moderation }

При добавлении как правило статус модерации ассета не зависит от содержимого, а только от статусов модерации родительских объектов: группы и кампании.

Обычно вычисление статуса производится в `AddOperationTypeSupport.beforeExecution`.

Пример: [BannerWithButtonAddOperationTypeSupport](https://a.yandex-team.ru/arc/trunk/arcadia/direct/core/src/main/java/ru/yandex/direct/core/entity/banner/type/button/BannerWithButtonAddOperationTypeSupport.java)


## Операция обновления { #op-update }

Код: [BannersUpdateOperation](https://a.yandex-team.ru/arc/trunk/arcadia/direct/core/src/main/java/ru/yandex/direct/core/entity/banner/service/BannersUpdateOperation.java).

Что делает операция:

- в несколько этапов проводит валидацию, делегируя конкретные проверки валидационным тайп-саппортам;
- в несколько этапов выполняет дополнительные действия, делегируя это операционным тайп-саппортам;
- обновляет баннеры (изменения которых успешно прошли валидацию), делегируя это репозиторию, который в свою очередь делегирует это репозиторным тайп-саппортам.

Особенности:

- работа с баннерами только одного клиента
- бизнес-логика рассчитана на то, что операция выполняется пользователем, а не системой
- работа от имени "оператора" — того, кто непосредственно делает запрос через внешний интерфейс (API, Web)

{% note warning "Проверка фич" %}

Для проверки доступности фич необходимо использовать список фич из контейнера (подробнее в разделе [Контейнеры](#container)), а не обращаться напрямую в `FeatureService`. Так гарантируется фиксированное состояние фич во всех частях операции.

{% endnote %}

### Воркфлоу операции обновления { #op-update-workflow }

Выполнение операции состоит из двух частей:

- подготовка, которая включает в себя валидацию (`AbstractUpdateOperation.prepare`);
- непосредственно применение изменений (`AbstractUpdateOperation.apply`).

#### Подготовка { #op-update-workflow-prepare }

На этапе подготовки в определенном порядке вызываются методы валидационных и операционных тайп-саппортов
(подробнее о типах тайп-саппортов в разделе [Бизнес-логика ассетов — тайп-саппорты](#asset-business-logic)).

{% note warning "На этапе подготовки не допускается изменение состояния БД" %}

Контракт операций декларирует, что изменения в базе данных производятся только на этапе применения изменений. Клиентский код может выполнить этап подготовки для получения результата валидации и при этом рассчитывать на то, что это не приведет к каким-либо изменениям в БД.

{% endnote %}

Подготовка состоит из следующих этапов:

1. _Заполнение контейнеров._ Подробнее в разделе [Контейнеры](#container).

1. _Превалидация._ Валидационным тайп-саппортам передаются потенциальные изменения баннеров ([ModelChanges](https://a.yandex-team.ru/arc/trunk/arcadia/direct/libs/model/src/main/java/ru/yandex/direct/model/ModelChanges.java)) в метод `UpdateValidationTypeSupport.preValidate`.

1. _Действия после превалидации._ Успешно прошедшие превалидацию изменения ([ModelChanges](https://a.yandex-team.ru/arc/trunk/arcadia/direct/libs/model/src/main/java/ru/yandex/direct/model/ModelChanges.java)) передаются в метод `UpdateOperationTypeSupport.onModelChangesValidated`. В этом методе могут выполняться дополнительные действия перед последующими этапами валидации.

1. _Валидация изменений относительно текущего состояния моделей в базе._ Успешно прошедшие превалидацию изменения ([ModelChanges](https://a.yandex-team.ru/arc/trunk/arcadia/direct/libs/model/src/main/java/ru/yandex/direct/model/ModelChanges.java)) и соответствующие им объекты из базы передаются в метод `UpdateValidationTypeSupport.validateBeforeApply`. В этом методе проверяется, что изменения баннеров валидны относительно текущего состояния в базе. Например, в [BannerWithCreativeUpdateValidationTypeSupport](https://a.yandex-team.ru/arc/trunk/arcadia/direct/core/src/main/java/ru/yandex/direct/core/entity/banner/type/creative/BannerWithCreativeUpdateValidationTypeSupport.java) проверяется, что размер креатива не меняется.

1. _Применение изменений._ Изменения ([ModelChanges](https://a.yandex-team.ru/arc/trunk/arcadia/direct/libs/model/src/main/java/ru/yandex/direct/model/ModelChanges.java)), успешно прошедшие предыдущие этапы валидации, применяются к соответствующим им объектам из базы, и таким образом формируются объекты [AppliedChanges](https://a.yandex-team.ru/arc/trunk/arcadia/direct/libs/model/src/main/java/ru/yandex/direct/model/AppliedChanges.java).

1. _Действия после применения изменений к моделям._ Примененные к баннерам изменения ([AppliedChanges](https://a.yandex-team.ru/arc/trunk/arcadia/direct/libs/model/src/main/java/ru/yandex/direct/model/AppliedChanges.java)) передаются операционным тайп-саппортам в метод `UpdateOperationTypeSupport.onChangesApplied`. Таким образом методу доступно как состояние моделей в базе, так и конечное состояние после применения изменений. На основе этой информации можно реализовывать дополнительную логику, в том числе модификацию самих `AppliedChanges`.

1. _Основная валидация._ Валидационным тайп-саппортам передается результат валидации баннеров с примененными изменениями в метод `UpdateValidationTypeSupport.validate`, но только тех баннеров, чьи изменения успешно прошли предшествующие этапы валидации. На данном этапе проводится валидация конечного состояния объектов. Это самый предпочтительный этап для проведения валидации, так как код валидации может работать непосредственно с моделями и от этого получается простым и универсальным для add и update.

1. _Действия после основной валидации._ Операционным тайп-саппортам передаются подходящие по типу баннеры, успешно прошедшие все предшествующие этапы валидации, в метод `UpdateOperationTypeSupport.onAppliedChangesValidated`. Это первый этап, в котором проводится работа с полностью валидными баннерами. Здесь их при необходимости можно подготовить к сохранению в базу.

{% note info "На этапе подготовки вызываются тайп-саппорты разных типов" %}

На этапе подготовки последовательно вызываются методы разных тайп-саппортов: `UpdateValidationTypeSupport` и `UpdateOperationTypeSupport`. В операционный тайп-саппорт передаются только объекты, успешно прошедшие все предшествующие этапы валидации. При этом порядок обращения к конкретным тайп-саппортам не определен.

{% endnote %}

{% note warning "В валидационных тайп-саппортах не допускается изменение моделей баннеров" %}

Такая договоренность необходима для четкого разделения обязанностей между тайп-саппортами. Её соблюдение облегчает поддержку и развитие продукта.

{% endnote %}

{% note tip "На каком этапе лучше делать валидацию?" %}

По умолчанию валидируется конечное состояние баннеров с примененными к ним изменениями в методе `UpdateValidationTypeSupport.validate` — валидировать состояние проще, чем изменения.
Если требуется проверить потенциальные изменения относительно текущего состояния баннеров в базе, то используйте метод `UpdateValidationTypeSupport.validateBeforeApply`. 
Если хочется отсечь невалидный баннер как можно раньше, то возможно вам подойдет `UpdateValidationTypeSupport.preValidate` (на этом этапе осуществляется проверка прав).

{% endnote %}

#### Применение изменений { #op-update-workflow-apply }

{% note info "Условие применения изменений" %}

Описываемые здесь этапы выполняются только в том случае, если валидация прошла успешно с учетом режима работы операции. В режиме `PARTIAL` нужен минимум один валидный объект. Режим `FULL` требует, чтобы все объекты были валидны. Если применение изменений невозможно, то ни один из последующих этапов не будет выполнен.

{% endnote %}

Применение изменений состоит из следующих этапов:

1. _Действия перед сохранением баннеров вне транзакции._ Примененные к баннерам изменения ([AppliedChanges](https://a.yandex-team.ru/arc/trunk/arcadia/direct/libs/model/src/main/java/ru/yandex/direct/model/AppliedChanges.java)) передаются операционным тайп-саппортам в метод `UpdateOperationTypeSupport.beforeExecution` до выполнения апдейта в БД. Этот метод может использоваться как для внесения _дополнительных_ изменений в базу, не относящихся непосредственно к изменению баннеров, так и для модификации самих `AppliedChanges` перед их сохранением в БД.

1. _Обновление статуса синхронизации с Баннерной Крутилкой (БК)._
Примененные к баннерам изменения ([AppliedChanges](https://a.yandex-team.ru/arc/trunk/arcadia/direct/libs/model/src/main/java/ru/yandex/direct/model/AppliedChanges.java)) передаются операционным тайп-саппортам в метод `UpdateOperationTypeSupport.needBsResync`.
Метод должен принять решение, требуют ли эти изменения пересинхронизации баннера с БК.
Если требуют — он должен вернуть `true`, в противном случае — `false`.
На основе этой информации и некоторых внутренних условий операция добавляет в `AppliedChanges` сброс статуса `statusBsSynced`.

1. _Обновление времени последнего изменения `LastChange`._
Примененные к баннерам изменения ([AppliedChanges](https://a.yandex-team.ru/arc/trunk/arcadia/direct/libs/model/src/main/java/ru/yandex/direct/model/AppliedChanges.java)) передаются операционным тайп-саппортам в метод `UpdateOperationTypeSupport.needLastChangeReset`.
Метод должен принять решение, требуют ли эти изменения сброса `LastChange`.
Если требуют — он должен вернуть `true`, в противном случае — `false`.
На основе этой информации операция добавляет в `AppliedChanges` обновление `LastChange`.

1. _Добавление информации в контейнер дополнительных действий_. У операционных тайп-саппортов вызывается метод `AddOperationTypeSupport.addToAdditionalActionsContainer`, в котором они могут добавить идентификаторы объектов в контейнер дополнительных действий (подробнее в разделе [Сервис дополнительных действий](#container-additional-actions)).

1. _Обновление статуса модерации `statusModerate`._
Примененные к баннерам изменения ([AppliedChanges](https://a.yandex-team.ru/arc/trunk/arcadia/direct/libs/model/src/main/java/ru/yandex/direct/model/AppliedChanges.java)) передаются операционным тайп-саппортам в метод `UpdateOperationTypeSupport.needModeration`.
Метод должен принять решение, требуют ли эти изменения переотправки баннера в модерацию.
Если требуют — он должен вернуть `true`, в противном случае — `false`.
На основе этой информации и некоторой дополнительной логики операция добавляет в `AppliedChanges` обновление статусов `statusModerate` и `statusPostModerate`.
Подробности в разделе [Статусы модерации баннера в операции обновления](#op-update-banner-moderation).

1. _Действия перед сохранением баннеров в транзакции._ Непосредственно перед этим шагом открывается транзакция. У операционных тайп-саппортов вызывается метод `UpdateOperationTypeSupport.beforeExecutionInTransaction`, куда передается контекст открытой транзакции `DSLContext dslContext`.

1. _Обновление баннеров в базе_. В транзакции вызывается соответствующий метод репозитория (подробнее о работе репозитория в разделе [Обновление](#repo-update)).

1. _Действия после сохранения баннеров в транзакции._ У операционных тайп-саппортов вызывается метод `UpdateOperationTypeSupport.updateRelatedEntitiesInTransaction`, куда передается контекст открытой транзакции `DSLContext dslContext`.

1. _Обработка контейнера дополнительных действий._ Сервис [BannerAdditionalActionsService](https://a.yandex-team.ru/arc/trunk/arcadia/direct/core/src/main/java/ru/yandex/direct/core/entity/banner/service/BannerAdditionalActionsService.java) выполняет дополнительные действия над объектами, добавленными в контейнер на четвертом шаге.

### Статусы модерации баннера в операции обновления { #op-update-banner-moderation }

При изменении баннера может потребоваться переотправить его в модерацию. Необходимость переотправки зависит от того, какие поля изменяются и каким образом. Например, если в заголовке удалить лишний пробел, то баннер не будет переотправлен в модерацию, а если заменить одно слово на другое, то будет.

Так же на изменения статуса баннера влияют и другие факторы: предыдущий статус баннера, статус кампании и другие.

Таким образом, факторы, которые влияют на статус модерации баннера (`ppc.banners.statusModerate`), можно поделить на две категории: непосредственно связанные с изменением конкретного поля — _внутренние факторы_, и любые другие — _факторы окружения_.

Вместе с изменением статуса модерации баннера могут потребоваться и другие изменения. Например, отправка группы в модерацию.

Алгоритм сброса статуса модерации баннеров при обновлении:

- Операция [BannersUpdateOperation](https://a.yandex-team.ru/arc/trunk/arcadia/direct/core/src/main/java/ru/yandex/direct/core/entity/banner/service/BannersUpdateOperation.java) передает изменения каждого баннера ([AppliedChanges](https://a.yandex-team.ru/arc/trunk/arcadia/direct/libs/model/src/main/java/ru/yandex/direct/model/AppliedChanges.java)) всем его тайп-саппортам в метод `UpdateOperationTypeSupport.needModeration`.
- Каждый тайп-саппорт принимает решение, должны ли изменения в полях интерфейса приводить к отправке баннера в модерацию;
если должны, то метод возвращает `true`, в противном случае — `false`.
Таким образом, данный метод отвечает за учёт описанных выше _внутренних факторов_ и игнорирует _факторы окружения_.
- Операция получает идентификаторы баннеров, для которых хотя бы один тайп-саппорт вернул `true`.
- Операция передает данные баннеров в [BannersUpdateModerationService](https://a.yandex-team.ru/arc/trunk/arcadia/direct/core/src/main/java/ru/yandex/direct/core/entity/banner/service/BannersUpdateModerationService.java)
- [BannersUpdateModerationService](https://a.yandex-team.ru/arc/trunk/arcadia/direct/core/src/main/java/ru/yandex/direct/core/entity/banner/service/BannersUpdateModerationService.java) делегирует обновление статусов каждого баннера одному из зарегистрированных процессоров, который выбирается по типу баннера. Если для определенного типа баннера не зарегистрирован специфичный процессор, то срабатывает дефолтный процессор [DefaultUpdateOperationModerationProcessor](https://a.yandex-team.ru/arc/trunk/arcadia/direct/core/src/main/java/ru/yandex/direct/core/entity/banner/type/moderation/update/DefaultUpdateOperationModerationProcessor.java).
- Каждый процессор получает флаг `needModeration`, вычисленный в тайп-саппортах на основе внутренних факторов ассетов, и выставляет новый статус модерации с учетом _факторов окружения_.

{% note info "Зачем нужны процессоры" %}

Есть две основные причины, по которым эта часть архитектуры реализована в виде отдельных процессоров. Одна из причин состоит в том, что в действительности есть обычная логика модерации, а есть экзотические вариации у некоторых типов баннеров. И такая архитектура позволяет им не смешиваться, при этом не препятствуя переиспользованию общего кода.

А вторая причина — это возможность для нового типа баннера сделать временное решение, чаще всего автоприемку, до тех пор, пока транспорт в модерацию или сам сервис Модерации не готовы работать с новым типом баннера. Самое важное, что при этом не меняется код модерации других типов баннеров! Когда автоприемка становится не нужна, просто удалите класс процессора, и для баннера заработает стандартная логика.

{% endnote %}

Все процессоры и абстрактные классы располагаются в директории [banner/type/moderation/update](https://a.yandex-team.ru/arc/trunk/arcadia/direct/core/src/main/java/ru/yandex/direct/core/entity/banner/type/moderation/update).

### Статус модерации ассета в операции обновления { #op-update-asset-moderation }

Здесь будет описан случай, когда у ассета есть собственный статус модерации. Если ассет является связкой с самостоятельной сущностью, то это статус модерации связки баннера с ней.<br/>
Примеры таких ассетов: связка с креативом ([ppc.banners_performance](https://direct-dev.yandex-team.ru/db/ppc/tables/banners_performance.html)), связка с турболендингом ([ppc.banner_turbolandings](https://direct-dev.yandex-team.ru/db/ppc/tables/banner_turbolandings.html)).

Логика установки статуса модерации ассета зависит от статуса модерации самого баннера. Чтобы она могла видеть и новый статус баннера и статус ассета, заводится агрегирующий интерфейс, объединяющий базовый интерфейс ассета и `BannerWithModerationStatuses`. Такие интерфейсы принято называть `"BannerWith" + <asset name> + "Moderation"`, например [BannerWithCreativeModeration](https://a.yandex-team.ru/arc/trunk/arcadia/direct/libs-internal/core-model/src/generated/java/ru/yandex/direct/core/entity/banner/model/BannerWithCreativeModeration.java).

В операционном тайп-саппорте для агрегирующего интерфейса создается экземпляр класса [BannerWithChildrenModerationProvider](https://a.yandex-team.ru/arc/trunk/arcadia/direct/core/src/main/java/ru/yandex/direct/core/entity/banner/service/moderation/BannerWithChildrenModerationProvider.java), как здесь: [BannerWithCreativeModerationUpdateOperationTypeSupport](https://a.yandex-team.ru/arc/trunk/arcadia/direct/core/src/main/java/ru/yandex/direct/core/entity/banner/type/creative/BannerWithCreativeModerationUpdateOperationTypeSupport.java). Ему в конструктор передаются процессоры для обработки именно этого ассера, которые автовайрятся с помощью Spring, а так же класс дефолтного процессора. Идея с процессорами здесь аналогична обработке [статуса модерации баннера](#op-update-banner-moderation).


## Контейнеры { #container }

Контейнеры представляют собой классы для передачи данных между разными частями кода баннеров. Методы всех типов тайп-саппортов принимают "контейнеры".

По механизму действия контейнеры делятся на два типа:

- контейнеры для передачи данных в тайп-саппорты
- контейнер дополнительных действий

### Контейнеры для передачи данных в тайп-саппорты { #container-input }

С помощью этих контейнеров передаются два вида данных.
Первый — это входные параметры операции, такие как `shard` и `ClientID`.
Второй — это данные из базы, которые требуются нескольким тайп-саппортам;
в этом случае в целях оптимизации числа запросов в базу они загружаются один раз на уровне операции и передаются в тайп-саппорты через контейнер.

Таким образом, если при разработке тайп-саппорта вам потребовались данные, которые уже загружает другой тайп-саппорт, подумайте о том, чтобы вынести данные в контейнер, а их загрузку на уровень операции.

### Контейнер дополнительных действий и его сервис { #container-additional-actions }

Этот механизм используется для оптимизации числа запросов в базу, когда различным тайп-саппортам требуется вносить одинаковые изменения, но над разными объектами.

Алгоритм работы:

- операционные тайп-саппорты складывают идентификаторы объектов в контейнер [BannerAdditionalActionsContainer](https://a.yandex-team.ru/arc/trunk/arcadia/direct/core/src/main/java/ru/yandex/direct/core/entity/banner/container/BannerAdditionalActionsContainer.java) в методе `addToAdditionalActionsContainer`;
- сервис [BannerAdditionalActionsService](https://a.yandex-team.ru/arc/trunk/arcadia/direct/core/src/main/java/ru/yandex/direct/core/entity/banner/service/BannerAdditionalActionsService.java) выполняет необходимые действия сразу для всех объектов в одной транзакции с сохранением баннеров.

Например, разные процессоры модерации могут принять решение переотправить группы в модерацию. Если бы каждый из них самостоятельно обновлял статус модерации групп, то было бы несколько однотипных запросов в базу. Вместо этого они складывают идентификаторы групп в общий контейнер, после чего статусы всех групп обновляются одним запросом.


## Валидация { #validation }

Подробнее об этапах валидации в разделах про подготовку в [воркфлоу операции добавления](#op-add-workflow-prepare) и [воркфлоу операции обновления](#op-update-workflow-prepare).

{% note tip "Как использовать общий код валидации в операциях добавления и обновления" %}

Чтобы использовать общий код, валидация должна проверять конечное состояние моделей, какое оно будет после применении потенциальных изменений.
В операции обновления такое состояние моделей доступно на самом позднем этапе валидации — в методе `UpdateValidationTypeSupport.validate`.
В операции добавления для симметрии используйте метод `AddValidationTypeSupport.validate`.
На практике в большинстве случаев удается использовать именно такой подход.

{% endnote %}

Для случая, когда валидация добавления и обновления работает с моделями, как описано в рекомендации выше, существует ряд договоренностей относительно структуры классов валидации. Эти договоренности созданы с учетом опыта реализации всех существующих ассетов, и учитывают множество кейсов. Они решают следующие задачи:

- простота переиспользования кода валидации;
- минимизация изменений в коде при изменении правил валидации (многие изменения получаются простыми);
- снижение рисков при внесении изменений за счет их простоты;
- тестируемость кода (так же есть рекомендации по структуре тестов);
- снижение порога входа за счет одинаковой структуры классов и их обязанностей.

### ValidatorProvider { #validation-provider }

Общей точкой входа в валидацию для добавления и обновления служит класс `*ValidatorProvider`:

- он является спринговым синглтоном и автовайрится в валидационные тайп-саппорты;
- в его обязанности входит подключение валидаторов для полей интерфейса;
- подгружает с использованием репозиториев дополнительные данные, требующиеся валидаторам;
- набор валидаторов и их параметры могут зависеть от конечного типа баннера, в этом случае в нем для каждого поля интерфейса реализуется условная логика с помощью конструкций `if-return` (`if-else` дает более сложный дифф при изменении кода);
- в нем могут быть подключены валидаторы по умолчанию, не зависящие от типа баннера;
- именуется в формате `имя интерфейса + ValidatorProvider`.

Простой эталонный пример: [BannerWithTurboLandingValidatorProvider](https://a.yandex-team.ru/arc/trunk/arcadia/direct/core/src/main/java/ru/yandex/direct/core/entity/banner/type/turbolanding/BannerWithTurboLandingValidatorProvider.java). <br/>
Пример с применением к одному и тому же полю разного набора валидаторов: [BannerWithCreativeValidatorProvider](https://a.yandex-team.ru/arc/trunk/arcadia/direct/core/src/main/java/ru/yandex/direct/core/entity/banner/type/creative/BannerWithCreativeValidatorProvider.java).

### Валидаторы { #validation-validator }

Правила валидации каждого поля интерфейса реализуются в виде отдельных валидаторов:

- в их обязанности входит наложение правил валидации (констрейнтов) на значение поля;
- они не являются спринговыми компонентами;
- они не содержат ссылок на спринговые компоненты;
- необходимые данные принимают при инициализации из `*ValidatorProvider`-а;
- при необходимости могут принимать параметры (флаги, константы);
- валидируют непосредственно значение поля (не интерфейс целиком);
- валидация одного поля интерфейса может быть распределена между несколькими валидаторами по смыслу или другим соображениям;
- имеют статический фабричный метод (или несколько) для органичного использования во fluent-интерфейсе библиотеки валидации;
- имеют имена в формате `Banner + [спецификатор] + <имя поля> + Validator` или `<тип баннера> + <имя поля> + Validator`, если валидация специфична для одного типа баннера.

Простой эталонный пример: [PermalinkIdValidator](https://a.yandex-team.ru/arc/trunk/arcadia/direct/core/src/main/java/ru/yandex/direct/core/entity/banner/type/organization/PermalinkIdValidator.java). <br/>
Пример посложнее: [BannerTextValidator](https://a.yandex-team.ru/arc/trunk/arcadia/direct/core/src/main/java/ru/yandex/direct/core/entity/banner/service/validation/BannerTextValidator.java)
(имя класса и расположение отличаются от стандартных, так как он валидирует поля нескольких ассетов — заголовка, дополнительного заголовка и текста).

### Констрейнты { #validation-constraint }

Общие констрейнты, не привязанные к конкретной бизнес-сущности хранятся в пакете [core/validation/constraints](https://a.yandex-team.ru/arc/trunk/arcadia/direct/core/src/main/java/ru/yandex/direct/core/validation/constraints).

Когда валидатору требуются специфические констрейнты, которых нет в общей библиотеке, их принято складывать в класс рядом с валидатором в виде статических фабричных методов.
Если валидатор называется `BannerCreativeValidator`, то класс с констрейнтами — `BannerCreativeConstraints`.

## Тестирование { #testing }

На верхнем уровне тесты делятся на несколько категорий относительно того, в каких тайп-саппортах находится тестируемая логика:

- тесты репозитория (чтение/создание/обновление);
- тесты валидации;
- тесты дополнительной логики в операционных тайп-саппортах.

Так же в тайп-саппортах могут использоваться дополнительные классы или модули, которые заслуживают собственных юнит-тестов. Их тестирование остается за рамками данного руководства.

{% note warning "Не вызывайте в тестах напрямую методы тайп-саппортов" %}

Вызывайте в тестах операцию целиком вместо обращения к методам тайп-саппортов.

Если будете вызывать тайп-саппорты, то тесты будут хрупкими, так как это очень подвижная часть. Тесты будут сложными, так как контейнеры придется инициализировать вручную. Тесты будут проверять логику не так, как она будет вызвана в операции, так как код инициализации контейнеров в тесте рано или поздно разойдется с кодом подготовки в операции.

{% endnote %}

{% note tip "Удобные абстрактные классы" %}

Если в тестах вызывается операция, используйте абстрактные классы (подробнее в разделе [Удобные абстрактные классы тестов](#testing-validation-convenient)).

{% endnote %}

### Тестирование репозитория { #testing-repo }

Отдельное тестирование уровня репозитория не требуется, когда ассет относится к баннеру как один-к-одному и используется один из абстрактных репозиториев (подробнее в разделе [Удобные абстрактные репозиторные тайп-саппорты](#repo-convenient)). В этом случае достаточно позитивных тестов на ассет в сборе (подробнее в разделе [Тестирование ассета в сборе](#testing-validation-all)).

Когда ассет относится к баннеру как один-ко-многим, тесты репозитория объединяются с позитивными тестами на ассет в сборе (подробнее в разделе [Тестирование ассета в сборе](#testing-validation-all)).
В этом случае позитивные тесты делаются параметризованными.
Так же в этом случае необходимы позитивные тесты, в которых в операцию передаются несколько баннеров — `<имя интерфейса> + MultiAddPositiveTest` и `<имя интерфейса> + MultiUpdatePositiveTest`.

Примеры:

- добавление нескольких баннеров: [BannerWithPixelsMultiAddPositiveTest](https://a.yandex-team.ru/arc/trunk/arcadia/direct/core/src/test/java/ru/yandex/direct/core/entity/banner/type/pixels/BannerWithPixelsMultiAddPositiveTest.java)
- обновление нескольких баннеров: [BannerWithPixelsMultiUpdatePositiveTest](https://a.yandex-team.ru/arc/trunk/arcadia/direct/core/src/test/java/ru/yandex/direct/core/entity/banner/type/pixels/BannerWithPixelsMultiUpdatePositiveTest.java)

### Тестирование валидации { #testing-validation }

{% note tip "Используйте параметризованные тесты" %}

Тесты валидации должны быть параметризованными, так как тест-кейсы отличаются друг от друга только данными, а алгоритм всегда один и тот же. Это дает большое преимущество в поддержке.

{% endnote %}

Тесты валидации представляют собой классическую пирамиду тестов:

- тесты констрейнтов (их больше всего);
- тесты валидаторов (меньше);
- тесты валидатор-провайдеров (не больше чем тестов констрейнтов);
- тесты операции в сборе (единицы).

#### Тесты констрейнтов { #testing-validation-constraint }

Задача тестов констрейнтов — максимально подробно проверить описываемые ими правила валидации.
Больше всего кейсов валидации проверяется именно этой категорией тестов.

Тесты констрейнтов, как и сами констрейнты, не зависят от спринговых компонентов. Это позволяет им работать быстро.

Каждый констрейнт тестируется в отдельном _параметризованном тесте_ (в отдельном классе). Несмотря на то что констрейнты одного валидатора могут находиться в одном классе, каждый констрейнт заслуживает отдельного класса тестов. Это облегчает поддержку. Правило именования тестов констрейнтов: `<имя класса с констрейнтами> + <имя констрейнта, может быть сокращенным> + Test`.

{% note tip %}

Попробуйте использовать базовые суперклассы в тестах констрейнтов, так вы получите максимальное переиспользование кода. Пример: [BannerTextConstraintsCommasAreBoundedTest](https://a.yandex-team.ru/arc/trunk/arcadia/direct/core/src/test/java/ru/yandex/direct/core/entity/banner/service/validation/BannerTextConstraintsCommasAreBoundedTest.java) и его базовый класс [BannerTextConstraintsBaseTest](https://a.yandex-team.ru/arc/trunk/arcadia/direct/core/src/test/java/ru/yandex/direct/core/entity/banner/service/validation/BannerTextConstraintsBaseTest.java).

{% endnote %}

#### Тесты валидаторов { #testing-validation-validator }

Задача тестов валидаторов — проверить, что все констрейнты подключены и правильно срабатывают.
Если валидатор принимает опции и имеет внутри условную логику, тесты так же должны это проверять.
Если код валидатора состоит только в линейном подключении констрейнтов, без параметров и условной логики, тест на него писать не обязательно (код теста будет сложнее, чем код валидатора).

Как правило, на валидатор пишется один параметризованный тест. В каждом тест-кейсе проверяется, что он вернул ожидаемый дефект или вернул результат валидации без дефектов. Моки в тестах валидаторов не используются. Пример: [BannerDisplayHrefValidatorTest](https://a.yandex-team.ru/arc/trunk/arcadia/direct/core/src/test/java/ru/yandex/direct/core/entity/banner/type/displayhref/BannerDisplayHrefValidatorTest.java).

В тестах валидаторов нет надобности повторно тестировать констрейнты. Когда в тестах валидатора проверяется возвращаемый констрейнтом дефект, на самом деле проверяется, что валидатор правильно его вызвал (в правильном случае, с правильными данными).

{% note tip %}

Давайте имена тест-кейсам параметризованного теста, как в примере выше.
Имена помогают как при поддержке тестов, чтобы понять их смысл, так и при запуске/отладке — для идентификации упавших тестов.

{% endnote %}

#### Тесты \*ValidatorProvider-ов { #testing-validation-provider }

Задача тестов валидатор-провайдеров — проверить логику, которая находится непосредственно в ValidatorProvider-е.

Выше определялись такие обязанности этих компонентов:

- загрузка необходимых для валидации данных;
- применение правильного набора валидаторов;
- передача валидаторам правильных данных и настроек;
- условная логика относительно типов баннера, группы, кампании, а так же фич клиента и других параметров.

Таким образом, тесты должны проверять, что:

- валидаторы вызываются, когда должны, и не вызываются, когда не должны
- валидаторы вызываются с правильными входными данными в зависимости от различных параметров (тип баннера, настройки и пр.)

{% note tip "Разделяйте тесты" %}

Если валидатор-провайдер обладает богатой бизнес-логикой, то его тесты можно организовать в виде нескольких классов с параметризованным тестом, чтобы не мешать в одну кучу разношерстные проверки. В этом случае тесты должны называться `<имя провайдера> + <краткое уточнение> + Test`.

{% endnote %}

{% note tip "Используйте Spring" %}

Так как ValidatorProvider является спринговым компонентом, желательно чтобы тесты работали с помощью спринга. Даже если в тот момент времени, когда пишутся тесты, спринг не нужен, возможно имеет смысл сразу сделать их такими, чтобы в будущем не приходилось кардинально изменять структуру теста.

{% endnote %}

{% note tip "Работайте в тестах с операцией" %}

Чтобы тест был простым и устойчивым к изменениям, в нем можно вызывать операцию, а не валидатор-провайдер. При этом тестироваться будет логика именно валидатор-провайдера.

{% endnote %}

Простой пример: [BannerWithTitleValidatorProviderTest](https://a.yandex-team.ru/arc/trunk/arcadia/direct/core/src/test/java/ru/yandex/direct/core/entity/banner/type/title/BannerWithTitleValidatorProviderTest.java).
Пример посложнее: [BannerWithTurboLandingValidatorProviderPayForConversionTest](https://a.yandex-team.ru/arc/trunk/arcadia/direct/core/src/test/java/ru/yandex/direct/core/entity/banner/type/turbolanding/BannerWithTurboLandingValidatorProviderPayForConversionTest.java)

### Тестирование логики операционных тайп-саппортов { #testing-validation-support }

{% note tip "Тестирование общей логики добавления и обновления" %}

Общую логику обновления и добавления лучше выносить в общие классы и тестировать их отдельно от операции.

{% endnote %}

Если в тайп-саппортах добавления есть специфическая логика, которой нет в обновлении и наоборот, то есть два варианта, как ее протестировать:

1. если логика не сильно связана с операцией, то вынести её в отдельный от тайп-саппортов класс и протестировать отдельно
(пример — тест "извлекателя текста": [CompoundTextExtractorTest](https://a.yandex-team.ru/arc/trunk/arcadia/direct/core/src/test/java/ru/yandex/direct/core/entity/banner/service/text/CompoundTextExtractorTest.java));
1. если логика сильно связана с операцией, тогда лучше тестировать через вызов операции
(пример — тест статуса модерации креатива: [DefaultBannerWithCreativeModerationForceModerateUpdatePositiveTest](https://a.yandex-team.ru/arc/trunk/arcadia/direct/core/src/test/java/ru/yandex/direct/core/entity/banner/type/creative/moderation/DefaultBannerWithCreativeModerationForceModerateUpdatePositiveTest.java)).

### Тестирование ассета в сборе { #testing-validation-all }

Задача тестов на ассет в сборе — проверить, что все компоненты подключены и в совокупности корректно отрабатывают.
Это обязательные тесты, так как они гарантируют работу основных сценариев операции.

Эти тесты делятся на четыре класса:

- позитивный тест операции добавления — `<имя интерфейса> + AddPositiveTest`
- позитивный тест операции обновления — `<имя интерфейса> + UpdatePositiveTest`
- негативный тест операции добавления — `<имя интерфейса> + AddNegativeTest`
- негативный тест операции обновления — `<имя интерфейса> + UpdateNegativeTest`

Позитивные тесты проверяют, что:

- валидные изменения сохраняются в базу (проверяется симметричным чтением после сохранения);
- вызывается дополнительная логика в операционных тайп-саппортах (проверяется только факт срабатывания, подробные тест-кейсы проверяются в специализированных тестах).

Негативные тесты проверяют, что при передаче в операцию невалидных изменений, операция возвращает дефект. Они не проверяют валидацию в деталях, только факт срабатывания.

{% note warning "Наличие данных для валидации" %}

Если код валидации требует связанные с баннером данные, необходимо проверить, что он корректно отработает, если этих данных не будет. Такое может случиться, например, в операции добавления: если для валидации ассета нужны данные группы, а указанная клиентом группа не существует. В этом случае валидация ассета не должна генерировать дефекты, так как они будут сгенерированы валидацией наличия группы.

{% endnote %}

{% note tip "Удобные абстрактные классы" %}

Для удобства написания тестов используйте абстрактные классы (подробнее в разделе [Удобные абстрактные классы тестов](#testing-validation-convenient)).

{% endnote %}

Примеры:

- позитивный тест добавления: [BannerWithBodyAddPositiveTest](https://a.yandex-team.ru/arc/trunk/arcadia/direct/core/src/test/java/ru/yandex/direct/core/entity/banner/type/body/BannerWithBodyAddPositiveTest.java)
- негативный тест добавления (в т.ч. проверяется работа с отсутствующей группой): [BannerWithBodyAddNegativeTest](https://a.yandex-team.ru/arc/trunk/arcadia/direct/core/src/test/java/ru/yandex/direct/core/entity/banner/type/body/BannerWithBodyAddNegativeTest.java)
- позитивный тест обновления: [BannerWithBodyUpdatePositiveTest](https://a.yandex-team.ru/arc/trunk/arcadia/direct/core/src/test/java/ru/yandex/direct/core/entity/banner/type/body/BannerWithBodyUpdatePositiveTest.java)
- негативный тест обновления: [BannerWithBodyUpdateNegativeTest](https://a.yandex-team.ru/arc/trunk/arcadia/direct/core/src/test/java/ru/yandex/direct/core/entity/banner/type/body/BannerWithBodyUpdateNegativeTest.java)

### Удобные абстрактные классы тестов { #testing-validation-convenient }

- [BannerAdGroupInfoAddOperationTestBase](https://a.yandex-team.ru/arc/trunk/arcadia/direct/core/src/test/java/ru/yandex/direct/core/entity/banner/type/BannerAdGroupInfoAddOperationTestBase.java) (пример позитивного теста: [BannerWithCreativeAddPositiveTest](https://a.yandex-team.ru/arc/trunk/arcadia/direct/core/src/test/java/ru/yandex/direct/core/entity/banner/type/creative/BannerWithCreativeAddPositiveTest.java); пример негативного теста: [BannerWithCreativeAddNegativeTest](https://a.yandex-team.ru/arc/trunk/arcadia/direct/core/src/test/java/ru/yandex/direct/core/entity/banner/type/creative/BannerWithCreativeAddNegativeTest.java))
- [BannerNewBannerInfoUpdateOperationTestBase](https://a.yandex-team.ru/arc/trunk/arcadia/direct/core/src/test/java/ru/yandex/direct/core/entity/banner/type/BannerNewBannerInfoUpdateOperationTestBase.java) (пример позитивного теста: [BannerWithImageUpdatePositiveTest](https://a.yandex-team.ru/arc/trunk/arcadia/direct/core/src/test/java/ru/yandex/direct/core/entity/banner/type/image/BannerWithImageUpdatePositiveTest.java); пример негативного теста: [BannerWithImageUpdateNegativeTest](https://a.yandex-team.ru/arc/trunk/arcadia/direct/core/src/test/java/ru/yandex/direct/core/entity/banner/type/image/BannerWithImageUpdateNegativeTest.java))


## Ссылки на инструкции
- [Поиск ассетов и их логики](howto-find-asset.md)
- [Переиспользование ассета](howto-reuse-asset.md)
- [Создание нового типа баннера](howto-new-banner.md)
