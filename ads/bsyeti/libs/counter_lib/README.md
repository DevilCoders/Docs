# Библиотека счетчиков
## Чтот такое счетчики?
Счетчики — это способ хранения информации в профилях, в Поведенческом (BigB, Eagle/Buzzard, bsyeti, etc) и Цезарaе (Caesar).  
Счетчики — это один из самых простых способов хранить информацию, получаемую из потока.  
Каждый счетчик — это сущность, которая хранит какое-то действительное значение по 64-битному ключу.  

То есть математически можно рассматривать счетчик как действительнозначную функцию:
```
counter: (ProfileId, CounterKey) -> Float,
```
где ProfileId -- внешний ключ, CounterKey -- внутренний ключ.
![storage scheme](https://jing.yandex-team.ru/files/igorsolovyev/Screen%20Shot%202021-10-13%20at%2012.48.00.png "Схема хранения")


#### Для чего стоит ипользовать счетчики.
Счетчики стоит использовать для аддитивных функций по каким-то ключам.  
Отлично подходит для того, чтобы посчитать, сколько раз профиль кликал по рекламе, чтобы посчитать сколько раз он просматривал каждый конкретный баннер.

#### Для чего не следует использоовать счетчики.
Счетчики не следует использовать для точных аналитических задач.  
Задачи "сколько раз происходило событие за последний час пользователь кликнул по каждому типу товаров" — плохо решается в рамках счетчиков без дополнительного кодинга.  
В таком случае лучше рассмотреть приблеженные решения таких задач, например несколько счетчиков по одному ключу с разной скоростью затухания.

#### Что есть в счетчиках
В счетчиках реализованы:

+ Контроль за временем жизни и размером

+ Суммиравоние с экспоненциальным затуханием

+ Несколько счетчиков по одному набору ключей

+ Достаточно компактный способ хранения в виде протобуфа

+ Библиотечка для линейного итерирования для питона и c++

+ Библиотечка для look up'ов и update'ов с кешированием

#### Основные понятия
+ профиль -- сущность, которая хранится в Buzzard/Caesar, связанная с каким-то уникальным идентификатором(ProfileID пользователя, BannerID баннера, PageID страницы, etc.)
+ счетчик -- тип данных, хранимых в профиле.  
  Семантически представляет из себя таблицу ключ -> значение.  
  Каждый счетчик имеет идентификатор `counter_id`.
+ ключи счетчика -- список значений, для которых в счетчике имеются какие-то данные.
+ пак счетчиков -- оптимизация формата хранения счетчиков.  
  Нужна для счетчиков, которые должны иметь одинаковые ключи. 
  В профиле может хранится любое количество паков счетчиков, эти паки обрабатываются независимо.


  

## Конфигурация

Конфиг счетчиков хранится в [в протбуф схеме](https://a.yandex-team.ru/arc/trunk/arcadia/ads/bsyeti/libs/primitives/counter_proto/counter_ids.proto).
В идеальном мире комментариев в нем должно хватать для понимания, но для примера разберем несколько частотных случаев.

Рассмотрим конфиг на примере подсчета числа открытий карточек заведений из Больших Яндекс Карт.  
Мы хотим суммировать число событий по отдельности для каждого заведения, поэтому в качестве ключа(`EngineNamespace`) указываем `EN_CATALOG_COMPANY_ID`.  
Также мы хотим, чтобы эти данные автоматически удалялись со временем, поэтому мы создаем парный счетчик времени.  
В нем будут хранится время последнего апдейта. Также он будет нужен для суммирования с затуханием.  
`ExpireDays: 30` -- означает, что через 30 дней неактивности счетчик будет удален.
`MaxRecords: 60` -- означает, что будут хранится не более шестидесяти записей.
```protobuf
    CI_DESKTOP_MAP_PERMALINK_CLICK_COUNT = 539 [
        (CounterDescription) = {
            EngineNamespace: EN_CATALOG_COMPANY_ID
            ValueFunction: VF_FLOAT
            IdFunction: IF_ID
            DecayFactor: 1
            TimeCounterId: CI_DESKTOP_MAP_PERMALINK_CLICK_TIME
            InputTypes: "redir"
            Description: 'Количество отркытий карточки из БЯК по permalinkу'
            UsageRestriction: UR_METRIKA_OWNED
        }
    ];

    CI_DESKTOP_MAP_PERMALINK_CLICK_TIME = 540 [
        (CounterDescription) = {
            EngineNamespace: EN_CATALOG_COMPANY_ID
            ValueFunction: VF_AGE
            IdFunction: IF_ID
            CleanUpSettings: {
                MaxRecords: 60
                ExpireDays: 30
            },
            NoOperation: true
            Description: 'Время отркытий карточки из БЯК по permalinkу'
            UsageRestriction: UR_METRIKA_OWNED
        }
    ];
```
+ ValueFunction -- это параметр, который определяет, что будет хранится в протбуфе, `float`/`fixed32`. `VF_FLOAT` — это `float`, `VF_AGE` - это `fixed32`.
+ EngineNamespace -- параметр, который указывает, что будет являтся ключами этого счетчика. Это значение должно быть из [атомов движка](https://a.yandex-team.ru/arc/trunk/arcadia/yabs/server/libs/lm/lm_atom.h). Они должны соответствовать тому, что на самом деле будет в счетчике, движок пытается лукапить счетчики по этому параметру. Примеры того, что может быть
    + PageID -- id страниц.
    + Gender -- пол.
    + BannerBMCategoryID -- категория баннера.
+ ExpireDays -- время, спустя которое счетчик будет удален.
+ MaxRecords -- если число ключей превышает этот параметр, то самые старые записи будут удалены. При наличи записей с одинаковыми временами, одну из которых нужно удалить будет удалена одна из них без дополнительных гарантий.
+ DecayFactor -- число, которое определяет, как будут суммироваться два разных события в счетчике.
    + Пусть у нас будут события `{ { v_i , t_i } | i : [1 .. n] }`
    + Тогда в счетчике будет `{ V := Sum { v_i * exp ^ ( - DecayFactor * (T - t_i) / 3600 / 24 / 7 ), i : [1..n] }, T := Max { t_i, i : [1..n] } }`
    + То есть событие величины `1.0`, которое случилось неделю назад, считается столь же "важным", как событие величины `exp ^ DecayFactor` случившееся только что.
+ UsageRestriction -- показывает, что этот счетчик имеет ограниченное применение, чтобы его использовать **нужно получить разрешение**. В силу различных причин, не существует возможности это обеспечить технически.

Стоит отметить, что можно использовать один счетчик-времени для нескольких счетчиков-значений. Тогда эти счетчики будут использовать общее множество ключей и общие времена.

Также стоит отметить, что ключ может быть составным. Это будет выглядеть следующим образом:
```protobuf
    CI_CLICKS_PAGE_IMP_COUNT = 156 [
        (CounterDescription) = {
            EngineNamespace: EN_PAGE_ID
            SecondaryEngineNamespace: EN_IMP_ID
            ValueFunction: VF_FLOAT
            IdFunction: IF_POLY2
```
То есть в качестве ключа будет использоваться хешфункция от каких-то базовых ключей.

По-умолчанию считается, что счетчик считается по профилю пользователя в Buzzard'е.  
Обратное можно указать следующим образом:
```protobuf
            ProfileType: PT_BANNER
```


**TODO: написать про NotGlued, Idf**

## Имплементация в коде

#### Как добавить данные
В данном разделе предполагается, что входные логи уже были добавлены в Caesar/Buzzard.  
Информация об этом есть в соответствующем разделе:

+ Caesar: https://wiki.yandex-team.ru/bigb/caesar/#dobavlenienovyxdannyx
+ Buzzard: https://wiki.yandex-team.ru/bigb/new-log
---
После того, как конфиг написан, пути немного расходятся в зависимости от того, куда пишется счетчик. 
### Caesar
В цезаре нужно найти подходящий граф. Предположим, что нас интересуют [баннерный граф](https://a.yandex-team.ru/arc/trunk/arcadia/ads/bsyeti/caesar/libs/graph/banner_graph.cpp).  
Сначала нужно убедится, что в профиле интересуещего нас типа имеется поле Counters, такого типа, в котором есть `repeated NBSYeti.TCounterPack PackedCounters`. Без этого в нужном профиле не будет сгенерирован код для счетчиков.

Находим в коде графа нужный нам [лог](https://a.yandex-team.ru/arc/trunk/arcadia/ads/bsyeti/caesar/libs/graph/banner_graph.cpp?rev=r8714659#L2322) и его [обработчик](https://a.yandex-team.ru/arc/trunk/arcadia/ads/bsyeti/caesar/libs/graph/banner_graph.cpp?rev=r8714659#L95). Предположим, что нас интересует визит-лог.  
Тогда, если в обработчике нет функции обновления счетчиков, то создаем ее.  
Размещать ее следует примерно [в этой папке](https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/counters/banner_counters.h?rev=6b4801200c25875c490f684f4763a6222df37a1f#L27).

Сам код по добавлению одного счетчика выглядит примерно так:

```c++
NBSYeti::TMutableCounters&& counters = profile->MutableCounters(); // получаем специальный мутатор для счетчиков

counters.Update(
    CI_MY_VERY_SPECIAL_COUNTER,
    event.GetFieldForCounterKey(),
    event.GetFieldForCounterValue(),
    event.GetFieldForCounterTime() /* время в секундах с начала эпохи */);
```

После этого стоит убедится, что выставлено удаление счетчиков. Примерно так как [здесь](https://a.yandex-team.ru/arc/trunk/arcadia/ads/bsyeti/caesar/libs/graph/banner_graph.cpp?rev=r8715335#L2618).

```c++
p->MutableCounters().Cleanup(now.Seconds(), true);
```

Без этого счетчики могут распухать, поскольку именно здесь происходит удаление старых ключей в счетчиках, а также ключей в счетчичках, если их оказалось больше максимально допустимого размера.  
Но не стоит очищать счетчики, если вы ничего туда не добавили.



### Buzzard

Нужно добавить коллектор или входной лог в [список входных типов](https://a.yandex-team.ru/arc/trunk/arcadia/ads/bsyeti/libs/collectors/counter.h?rev=r8583446#L34).

Затем нужно добавить обработчик для каждого счетчика, за образец можно взять [этот счетчик](https://a.yandex-team.ru/arc/trunk/arcadia/ads/bsyeti/libs/counter/counter_storage.h?rev=r8699180#L2193-2214).



## Использование

#### Как добавить клиента

В данном разделе предполагается, что у потребителя уже был настроен поход в Eagle/доступ к логу с профилем.  
Информация об этом есть в соответствующем разделе:

+ Как ходить в RealTime: https://wiki.yandex-team.ru/bigb/how-to-realtime
  + следует обратить внимание, что чтобы счетчики появились в ответе нужно указать соответствующий [киворд](https://a.yandex-team.ru/arc/trunk/arcadia/ads/bsyeti/eagle/config/clients.pb?rev=r8712606#L1436) и список нужных [счетчиков](https://a.yandex-team.ru/arc/trunk/arcadia/ads/bsyeti/eagle/config/clients.pb?rev=r8712606#L1441-1452), а затем добится от дежурного, чтобы он зарелизил конфиг.
+ Наши логи и таблички: https://wiki.yandex-team.ru/bigb/profile-logs

В любом случае, вы должны иметь протобуф такого [типа](https://a.yandex-team.ru/arc/trunk/arcadia/yabs/proto/user_profile.proto?rev=r8592909#L54).

---

Итак у нас есть протобуф мессадж с такой [схемой](https://a.yandex-team.ru/arc/trunk/arcadia/yabs/proto/user_profile.proto?rev=r8592909#L54), не важно, из лога или получен по запросу. Существует основной способ просмотра счетчиков на [c++](https://a.yandex-team.ru/arc/trunk/arcadia/ads/bsyeti/libs/counter_lib/counter_packer/counter_packer.h?rev=r8668055#L650) и на [python](https://a.yandex-team.ru/arc/trunk/arcadia/ads/bsyeti/libs/py_proto_counters/proto_counters.py).  
То, как пользоваться питоном вполне понятно из [ut](https://a.yandex-team.ru/arc/trunk/arcadia/ads/bsyeti/libs/py_proto_counters/ut/test.py).
Пример использования варианта для [плюсов](https://a.yandex-team.ru/arc/trunk/arcadia/ads/bsyeti/libs/counter_calcers/bigb_context.cpp?blame=true&rev=r8716578#L52-66).

Итератор для плюсов работает линейно.
Подходит для задач, где нет необходимости многократно искать одни и теже счетчики, а нужно единожды достать все нужные.
Для такого случая кажется, что принципиально лучше не получится, 

Если же по какой-то причине нужно многократно выполнять поиск конкретных ключей конкретных счетчиков, то нужно использовать такую [[хеш-таблицеподобную структуру](https://a.yandex-team.ru/arc/trunk/arcadia/ads/bsyeti/libs/counter_lib/counters.h?rev=r8713274#L65).  
Но важно отметить, что она использует дополнительную память для кеширования, поэтому в общем случае линейный поиск является предпочтительным.  
Также эта структура не является толерантной по отношению к смене формата.

Все прочие способы чтения счетчиков выполняются на свой страх и риск (смотри ниже про инварианты).

## Владение

#### Предыстория

В рекламе была классическая проблема — мы используем данные одних рекламодателей для рекламы других.  
Для того чтобы этого избежать, существует общерекламная механика владений. События, которые хочется иметь привязанными помечаются в логах `target_domain`, `target_tomain_md5`, `tdmd`, etc.

Эта механика поддержана также в счетчиках.

#### Механизм сброса владений

Как правило речь идет о какой-то сущности наподобие товара. Если мы имеем информацию, о том, что пользователь интресовался товаром *a* от рекламодателя **A**, тогда эта информация будет оставаться недоступной в счетчике.  
Если же есть информация о том, что пользователь интресовался товаром *a* от рекламодателя **B**, при этом времена этих событий отличаются менее, чем на `DropTargetDomainMd5Counters.MergePeriod` (180 дней на момент на 08.10.2021), тогда эти события (оба) будут перемещены в обычные счетчики, или, иными словами, владения будеут сняты.  
Если же альтернативного источника не поялвяется в течение `Tdmd5DeletePeriodSeconds` (5 дней на момент на 08.10.2021), то запись будет удалена.

Стоит также заметить, что если информация от разных рекламодателей пришла в разные профили;, то будучи оба запрошены в Eagle, профили объединятся так, что владение по общим ключам будет сброшено.

*tl;dr: Мы ждем, пока не получим альтернативным источник — тогда мы публикуем, в противном случае сносим через пять дней.*

#### Механизм работы
События со владениями хранятся отдельно, вне поля счетчиков. Поэтому счетчик с отложенными владениями можно спокойно использовать, так как в нем нет приватных данных.

### Использование в Buzzard

Для этого нужно добавить поле `MaxDelayedRecords` в настройки клинапа:

```protobuf
CleanUpSettings: {
    MaxRecords: 30
    ExpireDays: 60
    MaxDelayedRecords: 600
},
```

А также использовать функции

```c++
void FillTargetDomainMd5Updates(
    TUpdates& updates, ui64 namespaceValue, const TMaybe<ui64>& tdmd5, double updateValue = 1
);
void FillTargetDomainMd5Updates(
    TUpdates& updates, TVector<ui64>* namespaceValue, const TMaybe<ui64>& tdmd5, double updateValue = 1
);
void FillTargetDomainMd5Updates(
    TUpdates& updates, TVector<ui64>* namespaceValue, const TMaybe<ui64>& tdmd5, TVector<double>* updateValue
);
```

, где `tdmd5` — это `md5` от `target_domain`, вместо:

```c++
void FillUpdates(TUpdates& updates, ui64 namespaceValue, double updateValue = 1);
void FillUpdates(TUpdates& updates, TVector<ui64>* namespaceValue, double updateValue = 1);
void FillUpdates(TUpdates& updates, TVector<ui64>* namespaceValue, TVector<double>* updateValue);
```

соответственно. 
### Использование в Eagle

## Формат хранения

------------------
Счетчики хранятся профиле в виде repeated поля в протобуфе.
В зависимости от того, какие это счетчики, они имеют тип TCounterPack или Counter.
Counter является устаревшим типом, который мы, однако, отдаем в рамках совместимости.
Все новые клиенты должны получать счетчики исключительно в формате TCounterPack.
Схемы этих сообщений хранятся в [протобуфе message.proto](https://a.yandex-team.ru/arc/trunk/arcadia/ads/bsyeti/libs/counter_lib/proto/message.proto?blame=true)

Рассмотрим, как хранятся значения в TCounterPack'е.
Там есть три поля:
```protobuf
repeated uint64 counter_ids = 1 [packed = true];
repeated uint64 keys = 2 [packed = true];
repeated TValueType values = 3;
```
где TValueType, это oneof из нескольких типов repeated полей.

Существующие инварианты:
```c++
// Пак не пуст
pack.counter_ids_size() > 0
pack.keys_size() > 0
// Размеры полей с id и со значениями совпадают.
pack.counter_ids_size() == pack.values_size()
// В каждом из значений
for i in 0, .., pack.value_size()
    // число ключей и число значений совпадают
    pack.key_size() == max(pack.values(i).float_values()  .value_size(),
                           pack.values(i).double_values() .value_size(),
                           pack.values(i).fixed32_values().value_size(),
                           pack.values(i).fixed64_values().value_size()
                       )
    // есть только одно непустое значение
    pack.key_size() == pack.values(i).float_values()  .value_size() +
                       pack.values(i).double_values() .value_size() +
                       pack.values(i).fixed32_values().value_size() +
                       pack.values(i).fixed64_values().value_size()
```

То, какое значение будет лежать в поле с типом TValueType, можно определить при помощи функции:
```c++
    pack.values(i).GetValueCase()
```
Возвращаемое значение этой функции однозначно определяется `pack.counter_ids(i)`.
То есть, по id можно понять, какие значения там будут лежать.

На что нет гарантий:
1. Какие id будут лежать в одном паке.
   + Это деталь реализации, может менятся по соображениям компактфикации.
2. Как будут упорядочены паки в репитед поле.
    + Это деталь реализации, может менятся в по соображением компактности и скорости работы.
3. Как будут упорядочены ключи внутри пака.
    + Это деталь реализации, может менятся в по соображением компактности и скорости работы.

В силу вышесказаного можно представлять поле `values` в виде матрицы, в которой `pack.counter_ids_size()` строк и `pack.keys_size()` столбцов.

Рассмотрим пример:
```json
{
    "counter_ids": [200, 201],
    "keys": [1000001, 1000002, 1000003],
    "values": [
        {
            "float_values" : {
                "value": [0.1, 0.2, 0.3]
            }
        },
        {
            "fixed32_values" : {
                "value": [1500000001, 1500000002, 1500000003]
            }
        }
    ]
}
```

Тогда можно считать, что в паке содержится такая табличка:
|        | key 1000001 | key 1000002 | key 1000003 |
| ------ | ----------: | ----------: | ----------: |
| id 200 |         0.1 |         0.2 |         0.3 |
| id 201 |  1500000001 |  1500000002 |  1500000003 |
![storage scheme2](https://jing.yandex-team.ru/files/igorsolovyev/Screen%20Shot%202021-10-13%20at%2012.48.07.png "Схема хранения2")
![storage scheme3](https://jing.yandex-team.ru/files/igorsolovyev/Screen%20Shot%202021-10-13%20at%2012.48.14.png "Схема хранения3")

## TCounters и TMutableCounters
**TBD**
