# 4.11.1

**PR:** [#2663215](https://a.yandex-team.ru/review/2663215)
**Author:** @robot-metatron **Date:** 2022-06-28

AmpHtml

обновлен apiary-annex

# 4.11.0

**PR:** [#2628400](https://a.yandex-team.ru/review/2628400)
**Author:** @robot-metatron **Date:** 2022-06-20

Откатывает ломающие изменения

### Usage

none

# 4.10.2

**PR:** [#2650527](https://a.yandex-team.ru/review/2650527)
**Author:** @robot-metatron **Date:** 2022-06-20

Обновление зависимостей

### Updates

  * `@yandex-market/declarations`: [3.1.3](../../shared/declarations/changelog.md#313) (was [3.1.2](../../shared/declarations/changelog.md#312))

# 4.10.1

**PR:** [#2620413](https://a.yandex-team.ru/review/2620413)
**Author:** @anseal **Date:** 2022-06-08

[[https://st.yandex-team.ru/MARKETFRONTECH-4482]]

1) testament завязывается на детали внутренней реализации (приватная _selectStoreByWidgetSource)
2) testament тестирует виждеты в изоляции, не создавая полноценных html-страниц, и поэтому может создавать react-виждеты без static-родителей (что невозможно в marketfront)

# 4.10.0

**PR:** [#2595101](https://a.yandex-team.ru/review/2595101)
**Author:** @hurtsok **Date:** 2022-06-01

Dynamic Widgets version 2

Добавилась возможность грузить виджеты по требованию(например по клику пользовател) и гарантированный
рендеринг после доставки артефактов. В первой имплементации была гонка: виджет мог загрузиться позже, а рендерить
начинали раньше и т.д

### Usage

1) В описании виджета, который будет через Slot рендерить динамический нужно указать, что он от него зависит:
```javascript
// dynamicWidget/index.js
export default Widget.describe({
    name: '@DynTest',
})

// commonWidget/index.js
Widget.describe({
    name: '@Test',
    dependencies: {
        dynWidgets: {
            '@DynTest': import('/path/to/dynamicWidget.js'),
        }
    }
})
```

2) Далее уже в котнроллере этого виджета создать **slot** под динамически импортируемый(важно указать bare = true и dynamic = true)

```javascript
// commonWidget/controller.js
import DynamicWidget from '/path/to/dynamicWidget.js'

export default function(ctx) {
    return {
        slots: {
            testDymanic: DynamicWidget.create(ctx, {}, {bare: true, dynamic: true})
        }
    }
}
```

3) Вставить slot во view. В примере ниже мы вставляем его после действия пользователя, таким 
   образом работает code-spliting и зависимости виджета загружаются по требованию

```javascript
// commonWidget/view.js
import React from 'react';
import {Slot} from '@yandex-market/apiary'; 

export default class View extends React.Component {
    onClick = () => {
        this.setState({renderDynamic: true});
    }
    
    render() {
        
        return (
            <div>
                Some Text here
                <button onClick={this.onClick}>Render Widget</button>
                {this.state.renderDynamic && <Slot name="testDymanic">}
            </div>
        )    
    }
}

```

# 4.9.1

**PR:** [#2587715](https://a.yandex-team.ru/review/2587715)
**Author:** @bykhovtsev **Date:** 2022-06-01

Обновление зависимостей

### Updates

  * `@yandex-market/server-exps`: [2.1.1](../server-exps/changelog.md#211) (was [2.1.0](../server-exps/changelog.md#210))

# 4.9.0

**PR:** [#2536350](https://a.yandex-team.ru/review/2536350)
**Author:** @anseal **Date:** 2022-05-31

Добавляем возможность откладывать гидрацию виждетов до заданных DOM-событий в виджете или до заданных Redux-экшенов

### Usage

Вернуть из контроллера `wakeUpOn: { domEvents: ['click', ...etc], reduxActions: [...]}`

# 4.8.0

**PR:** [#2585474](https://a.yandex-team.ru/review/2585474)
**Author:** @xavescor **Date:** 2022-05-30

Откат механизма отмены

### Usage

--

# 4.7.0

**PR:** [#2528234](https://a.yandex-team.ru/review/2528234)
**Author:** @xavescor **Date:** 2022-05-20

Добавлена публичная поддержка событий в апиари.
Расширен контракт контекста. Если вы обновляяетесь вместе с mandrel, то проблем не будет

### Usage

По использованию читай документацию. Раздел "Серверные события"

### Updates

  * `@yandex-market/server-exps`: [2.1.0](../server-exps/changelog.md#210) (was [2.0.5](../server-exps/changelog.md#205))

# 4.6.0

**PR:** [#2549557](https://a.yandex-team.ru/review/2549557)
**Author:** @smelukov **Date:** 2022-05-20

[undefined](https://st.yandex-team.ru/undefined) - undefined - очистка рантайма через метод `Runtime.destroy()`

### Usage

[undefined](https://st.yandex-team.ru/undefined) - undefined - используется для изолированного тестирования виджетов

# 4.5.0

**PR:** [#2489763](https://a.yandex-team.ru/review/2489763)
**Author:** @gluhovroma **Date:** 2022-05-05

**Обновил babel и его плагины до последних версий [[MARKETFRONT-83092]]**

### Usage

**Обновите babel в своих проектах [[MARKETFRONT-83092]]**

# 4.4.19

**PR:** [#2505309](https://a.yandex-team.ru/review/2505309)
**Author:** @gheljenor **Date:** 2022-04-27

[undefined](https://st.yandex-team.ru/undefined) - undefined

### Updates

  * `@yandex-market/invariant`: [1.1.8](../invariant/changelog.md#118) (was [1.1.7](../invariant/changelog.md#117))
  * `@yandex-market/server-exps`: [2.0.5](../server-exps/changelog.md#205) (was [2.0.4](../server-exps/changelog.md#204))
  * `@yandex-market/logger-src`: [3.0.13](../logger/changelog.md#3013) (was [3.0.12](../logger/changelog.md#3012))

# 4.4.18

**PR:** [#2495391](https://a.yandex-team.ru/review/2495391)
**Author:** @maslov-rn **Date:** 2022-04-25

Обновление зависимостей

# 4.4.17

**PR:** [#2464128](https://a.yandex-team.ru/review/2464128)
**Author:** @gheljenor **Date:** 2022-04-13

Обновление зависимостей

### Updates

  * `@yandex-market/declarations`: [3.1.2](../../shared/declarations/changelog.md#312) (was [3.1.1](../../shared/declarations/changelog.md#311))

# 4.4.16

**PR:** [#2463913](https://a.yandex-team.ru/review/2463913)
**Author:** @gheljenor **Date:** 2022-04-13

Обновление зависимостей

### Updates

  * `@yandex-market/declarations`: [3.1.1](../../shared/declarations/changelog.md#311) (was [3.1.0](../../shared/declarations/changelog.md#310))

# 4.4.15

**PR:** [#2460308](https://a.yandex-team.ru/review/2460308)
**Author:** @gheljenor **Date:** 2022-04-13

[TOARCADIA-955](https://st.yandex-team.ru/TOARCADIA-955) - Перенос в Аркадию: git@github.yandex-team.ru:market/monomarket.git

### Updates

  * `@yandex-market/invariant`: [1.1.7](../invariant/changelog.md#117) (was [1.1.6](../invariant/changelog.md#116))
  * `@yandex-market/server-exps`: [2.0.4](../server-exps/changelog.md#204) (was [2.0.3](../server-exps/changelog.md#203))
  * `@yandex-market/logger-src`: [3.0.12](../logger/changelog.md#3012) (was [3.0.11](../logger/changelog.md#3011))

# 4.4.14

**PR:** [#1012](https://github.yandex-team.ru/market/monomarket/pull/1012)
**Author:** @bykhovtsev **Date:** 2022-04-06

MARKETFRONT-77121 Выкатываем прогрессивную гидрацию в Маркет. Обновляем документацию

# 4.4.13

**PR:** [#970](https://github.yandex-team.ru/market/monomarket/pull/970)
**Author:** @maslov-rn **Date:** 2022-03-31

Правка прекомитной проверки check-flow-files

# 4.4.12

**PR:** [#951](https://github.yandex-team.ru/market/monomarket/pull/951)
**Author:** @gheljenor **Date:** 2022-03-28

Обновление зависимостей

### Updates

  * `@yandex-market/invariant`: [1.1.6](../invariant/changelog.md#116) (was [1.1.5](../invariant/changelog.md#115))
  * `@yandex-market/server-exps`: [2.0.3](../server-exps/changelog.md#203) (was [2.0.2](../server-exps/changelog.md#202))
  * `@yandex-market/logger-src`: [3.0.11](../logger/changelog.md#3011) (was [3.0.10](../logger/changelog.md#3010))
  * `@yandex-market/yammy`: [3.0.0](../../scripts/yammy/changelog.md#300) (was [2.15.4](../../scripts/yammy/changelog.md#2154))
  * `@yandex-market/yammy-lib`: [1.4.1](../yammy-lib/changelog.md#141) (was [1.4.0](../yammy-lib/changelog.md#140))
  * `@yandex-market/s3`: [1.1.2](../../scripts/s3/changelog.md#112) (was [1.1.1](../../scripts/s3/changelog.md#111))

# 4.4.11

**PR:** [#972](https://github.yandex-team.ru/market/monomarket/pull/972)
**Author:** @gheljenor **Date:** 2022-03-28

[MARKETFRONTECH-3877](https://st.yandex-team.ru/MARKETFRONTECH-3877) - Настроить генерацию симлинков скриптами в монорепе

# 4.4.10

**PR:** [#854](https://github.yandex-team.ru/market/monomarket/pull/854)
**Author:** @as-kondratev **Date:** 2022-03-10

Обновление зависимостей

### Updates

  * `@yandex-market/declarations`: [3.1.0](../../shared/declarations/changelog.md#310) (was [3.0.2](../../shared/declarations/changelog.md#302))

# 4.4.9

**PR:** [#866](https://github.yandex-team.ru/market/monomarket/pull/866)
**Author:** @bykhovtsev **Date:** 2022-02-24

Учим апиари делать реакт-поддерево виджета делать статичным с 
помощью компонента обертки. 

В момент гидрации запоминаем innerHTML таких оберток, а на этапе отрисовки
вставляем эту верстку вместо отрисовки реактом. При последующих отрисовках 
рисуем честно реактом

Экономия получается на 
- подключении колбэков, 
- редакс-обновлениях стора (коннекторы не работают, перерсовки не происходят при приходе патчей)

Минусы
- Лишний `<div>`, которого требует `dangerouslySetInnerHTML`
- Если бы верстка была оптимальной, такие приседания не нужны

# 4.4.8

**PR:** [#806](https://github.yandex-team.ru/market/monomarket/pull/806)
**Author:** @asvasilenko **Date:** 2022-02-17

[MARKETFRONT-71352](https://st.yandex-team.ru/MARKETFRONT-71352) - добавит .idea в gitignore Сделал отдельные функции для обработки таймингов виджетов и получения дельты метрик stuffing и hydrating

# 4.4.7

**PR:** [#797](https://github.yandex-team.ru/market/monomarket/pull/797)
**Author:** @dv-mikhaylov **Date:** 2022-02-03

Добавлена прекоммитная проверка check-flow-files, которая сравнивает файл с разрешением ts в папке src и ищет такой же файл в папке flow https://st.yandex-team.ru/MARKETFRONTECH-3273

### Updates

  * `@yandex-market/check-flow-files`: [1.0.1](../../scripts/check-flow/changelog.md#101) (was [1.0.0](../../scripts/check-flow/changelog.md#100))

# 4.4.6

**PR:** [#810](https://github.yandex-team.ru/market/monomarket/pull/810)
**Author:** @gheljenor **Date:** 2022-01-31

[MARKETFRONTECH-3151](https://st.yandex-team.ru/MARKETFRONTECH-3151) - [Монорепа] Обновление nodejs 12 -> 14/16

### Updates

  * `@yandex-market/error`: [1.5.1](../error/changelog.md#151) (was [1.5.0](../error/changelog.md#150))
  * `@yandex-market/invariant`: [1.1.5](../invariant/changelog.md#115) (was [1.1.4](../invariant/changelog.md#114))

# 4.4.5

**PR:** [#788](https://github.yandex-team.ru/market/monomarket/pull/788)
**Author:** @nkiyko **Date:** 2022-01-20

Обновление версий зависимостей

### Updates

  * `@yandex-market/invariant`: [1.1.4](../invariant/changelog.md#114) (was [1.1.3](../invariant/changelog.md#113))
  * `@yandex-market/server-exps`: [2.0.2](../server-exps/changelog.md#202) (was [2.0.1](../server-exps/changelog.md#201))
  * `@yandex-market/logger-src`: [3.0.10](../logger/changelog.md#3010) (was [3.0.9](../logger/changelog.md#309))

# 4.4.4

**PR:** [#603](https://github.yandex-team.ru/market/monomarket/pull/603)
**Author:** @bykovski-ilya **Date:** 2021-12-21

**Починил ошибку в зависимости пакета - openapi-to-bcm**

# 4.4.3

**PR:** [#640](https://github.yandex-team.ru/market/monomarket/pull/640)
**Author:** @maslov-rn **Date:** 2021-12-08

Убрал серверный эксперимент apiary_chain_context

# 4.4.2

**PR:** [#581](https://github.yandex-team.ru/market/monomarket/pull/581)
**Author:** @juleari **Date:** 2021-11-23

[MARKETFRONTECH-3408](https://st.yandex-team.ru/MARKETFRONTECH-3408) - Починить сборки

### Updates

  * `@yandex-market/invariant`: [1.1.3](../invariant/changelog.md#113) (was [1.1.2](../invariant/changelog.md#112))
  * `@yandex-market/server-exps`: [2.0.1](../server-exps/changelog.md#201) (was [2.0.0](../server-exps/changelog.md#200))
  * `@yandex-market/logger-src`: [3.0.9](../logger/changelog.md#309) (was [3.0.8](../logger/changelog.md#308))

# 4.4.1

**PR:** [#528](https://github.yandex-team.ru/market/monomarket/pull/528)
**Author:** @mtvv **Date:** 2021-11-12

Добавил описание мода withMissmatch

# 4.4.0

**PR:** [#496](https://github.yandex-team.ru/market/monomarket/pull/496)
**Author:** @maslov-rn **Date:** 2021-10-29

Добавил в стратегию параметр widgetsBlacklist для процессинга всех виджетов, кроме указанных id

### Usage

Без изменений

# 4.3.2

**PR:** [#423](https://github.yandex-team.ru/market/monomarket/pull/423)
**Author:** @juleari **Date:** 2021-10-21

[MARKETFRONTECH-3236](https://st.yandex-team.ru/MARKETFRONTECH-3236) - Починить парсинг тикета

# 4.3.1

**PR:** [#352](https://github.yandex-team.ru/market/monomarket/pull/352)
**Author:** @fenruga **Date:** 2021-10-13

Обновление зависимостей

### Updates

  * `@yandex-market/declarations`: [3.0.2](../../shared/declarations/changelog.md#302) (was [3.0.1](../../shared/declarations/changelog.md#301))

# 4.3.0

**PR:** [#410](https://github.yandex-team.ru/market/monomarket/pull/410)
**Author:** @maslov-rn **Date:** 2021-10-07

Создание копии контекста для контроллера виджета, необходимой для сохранения имени виджета

Возможно что-то поломается из-за копии контекста + возрастет потребление памяти,
запускаем серверным экспериментом флаг: apiary_chain_context

Добавил в зависимости apiary мини-библиотеку для работы с конфигом серверных экспов

Добавил тест для цепочки WidgetName<WidgetId | null>->ResourceName

### Usage

В объекте context._page доступны поля widgetId, widgetName

### Updates

  * `@yandex-market/server-exps`: [2.0.0](../server-exps/changelog.md#200) (was [1.0.0](../server-exps/changelog.md#100))

# 4.2.3

**PR:** [#424](https://github.yandex-team.ru/market/monomarket/pull/424)
**Author:** @gheljenor **Date:** 2021-10-06

Обновление зависимостей

# 4.2.2

**PR:** [#320](https://github.yandex-team.ru/market/monomarket/pull/320)
**Author:** @ashwets **Date:** 2021-09-15

Обновление зависимостей

### Updates

  * `@yandex-market/invariant`: [1.1.2](../invariant/changelog.md#112) (was [1.1.1](../invariant/changelog.md#111))

# 4.2.1

**PR:** [#209](https://github.yandex-team.ru/market/monomarket/pull/209)
**Author:** @pavelko95 **Date:** 2021-09-15

Обновление версий зависимостей

### Updates

  * `@yandex-market/invariant`: [1.1.1](../invariant/changelog.md#111) (was [1.1.0](../invariant/changelog.md#110))

# 4.2.0

**PR:** [#313](https://github.yandex-team.ru/market/monomarket/pull/313)
**Author:** @ivan-afanasov **Date:** 2021-09-10

[MARKETFRONT-56175](https://st.yandex-team.ru/MARKETFRONT-56175) - Пробрасывает все поля ошибки ServerError из апиари в поле extra для попадания полей в  extra_keys и extra-values TSKV логов и в кликхаус

### Usage

В ошибках ServerError теперь появилось поле extra. Оно заполняется автоматически, контракты дочерних ошибок не поменялись.

### Updates

  * `@yandex-market/error`: [1.5.0](../error/changelog.md#150) (was [1.4.6](../error/changelog.md#146))
  * `@yandex-market/invariant`: [1.1.0](../invariant/changelog.md#110) (was [1.0.5](../invariant/changelog.md#105))

# 4.1.1

**PR:** [#206](https://github.yandex-team.ru/market/monomarket/pull/206)
**Author:** @antonk52 **Date:** 2021-09-06

Обновление зависимостей

### Updates

  * `@yandex-market/invariant`: [1.0.5](../invariant/changelog.md#105) (was [1.0.4](../invariant/changelog.md#104))

# 4.1.0

**PR:** [#234](https://github.yandex-team.ru/market/monomarket/pull/234)
**Author:** @nickshevr **Date:** 2021-08-16

* под флагом перестаем считать дифф патчей и сыпать ошибкой

### Usage

Выставить флаг minimize_logs в серверных экспериментах

# 4.0.8

**PR:** [#207](https://github.yandex-team.ru/market/monomarket/pull/207)
**Author:** @juleari **Date:** 2021-08-09

Обновление зависимостей

### Updates

  * `@yandex-market/invariant`: [1.0.4](../invariant/changelog.md#104) (was [1.0.3](../invariant/changelog.md#103))

# 4.0.7

**PR:** [#222](https://github.yandex-team.ru/market/monomarket/pull/222)
**Author:** @juleari **Date:** 2021-08-09

[MARKETFRONTECH-2993](https://st.yandex-team.ru/MARKETFRONTECH-2993) - [Монорепа] Починить ссылки в ченжлогах

# 4.0.6

**PR:** [#215](https://github.yandex-team.ru/market/monomarket/pull/215)
**Author:** @gheljenor **Date:** 2021-08-04

[MARKETFRONTECH-2974](https://st.yandex-team.ru/MARKETFRONTECH-2974) - [Монорепа] Убираем скрипты из генерируемых пакетов

# 4.0.5

**PR:** [#212](https://github.yandex-team.ru/market/monomarket/pull/212)
**Author:** @bykhovtsev **Date:** 2021-08-04

Фикс, исправляет поведение, при котором опустевшая очередь снова начинает откладывать исполнение на startDelay
Если очередь уже стартовала однажды, то считаем, что рантайм уже работает, и нет смысла задерживаться

# 4.0.4

**PR:** [#201](https://github.yandex-team.ru/market/monomarket/pull/201)
**Author:** @gheljenor **Date:** 2021-08-02

Изменение версий зависимостей

### Updates

  * `@yandex-market/invariant`: [1.0.3](../invariant/changelog.md#103) (was [1.0.2](../invariant/changelog.md#102))
  * `@yandex-market/declarations`: [3.0.1](../../shared/declarations/changelog.md#301) (was [3.0.0](../../shared/declarations/changelog.md#300))

# 4.0.3

**PR:** [#205](https://github.yandex-team.ru/market/monomarket/pull/205)
**Author:** @dgudenkov **Date:** 2021-07-30

- убрал саппресы flow

### Updates

  * `@yandex-market/declarations`: [3.0.0](../../shared/declarations/changelog.md#300) (was [2.0.0](../../shared/declarations/changelog.md#200))

# 4.0.2

**PR:** [#175](https://github.yandex-team.ru/market/monomarket/pull/175)
**Author:** @loyd **Date:** 2021-07-26

Обновление зависимостей

### Updates

  * `@yandex-market/declarations`: [2.0.0](../../shared/declarations/changelog.md#200) (was [1.0.0](../../shared/declarations/changelog.md#100))

# 4.0.1

**PR:** [#189](https://github.yandex-team.ru/market/monomarket/pull/189)
**Author:** @gheljenor **Date:** 2021-07-26

Изменён формат описания времени сборки

### Updates

  * `@yandex-market/error`: [1.4.6](../error/changelog.md#146) (was [1.4.5](../error/changelog.md#145))
  * `@yandex-market/invariant`: [1.0.2](../invariant/changelog.md#102) (was [1.0.1](../invariant/changelog.md#101))

# 4.0.0

**PR:** [#168](https://github.yandex-team.ru/market/monomarket/pull/168)
**Author:** @avdotion **Date:** 2021-07-21

Обновление версий зависимостей

### Usage

Ничего не поменялось

### Migration

Обновите `@yandex-market/declarations` в связанных проектах

### Updates

  * `@yandex-market/declarations`: [1.0.0](../../shared/declarations/changelog.md#100) (was [0.22.1](../../shared/declarations/changelog.md#0221))

# 3.4.1

**PR:** [#165](https://github.yandex-team.ru/market/monomarket/pull/165)
**Author:** @antsa4 **Date:** 2021-07-16

Обновление версий зависимостей

### Updates

  * `@yandex-market/invariant`: [1.0.1](../invariant/changelog.md#101) (was [1.0.0](../invariant/changelog.md#100))

# 3.4.0

**PR:** [#158](https://github.yandex-team.ru/market/monomarket/pull/158)
**Author:** @dgudenkov **Date:** 2021-07-16

Добавил action `hardUpdateCollections` для "жесткого" обновления коллекций. Грубо говоря этот экшн замещает текущий стейт коллекций коллекциями из патча

### Usage

```javascript
import {hardUpdateCollections} from '@yandex-market/apiary';
...
hardUpdateCollections({
    collection1: newCollection1Value,
    collection2: {
        key: 'newValue'
    },
});
```

# 3.3.0

Обновлен `@yandex-market/invariant`.

### Usage

При обновлении обнови и `invariant`.

### Updates

  * `@yandex-market/invariant`: [1.0.0](../invariant/changelog.md#100) (was [0.5.0](../invariant/changelog.md#050))

# 3.2.3

Удалил setImmediate с клиента

### Updates

  * `@yandex-market/invariant`: [0.5.0](../invariant/changelog.md#050) (was [0.4.2](../invariant/changelog.md#042))

# 3.2.2

Проставлено время сборки

### Updates

  * `@yandex-market/invariant`: [0.4.2](../invariant/changelog.md#042) (was [0.4.1](../invariant/changelog.md#041))
  * `@yandex-market/yammy`: [2.0.0](../../scripts/yammy/changelog.md#200) (was [1.15.0](../../scripts/yammy/changelog.md#1150))

# 3.2.1

Добавлено правило санитайзинга '<!' в UNSAFE_CHARS_RE

# 3.2.0

Для непродакшен среды оборачиваем `Provider` реакта на клиенте в `HOC` у которого правильно задан `displayName`.
Благодаря этому, в react-dev-tools отображается понятное дерево реакт-компонентов

### Usage

..

# 3.1.1

Поправил декларации flow-типов: поддержаны изменения из 3.1.0

# 3.1.0

Добавляет возможность использовать очередь с приоритетами для гидрации виджетов

### Usage

В контроллере виджета передать `hydrationPriority`
На старт рантайма Апиари передать опции очереди 
```typescript
type Options = {
    /* ... */
    useHydrationHeap: {
        priorityForceStart?: number,
        startDelay?: number,
    }
}
```

# 3.0.4

Обновление зависимостей

### Updates

  * `@yandex-market/invariant`: [0.4.1](../invariant/changelog.md#041) (was [0.4.0](../invariant/changelog.md#040))
  * `eslint-plugin-stout`: [1.0.4](../../tools/eslint-plugin-stout/changelog.md#104) (was [1.0.3](../../tools/eslint-plugin-stout/changelog.md#103))

# 3.0.3

* переходим на тег noframes для apiary-patch

# 3.0.2

Обновление зависимостей

# 3.0.1

Добавлено правило санитайзинга '<!' , для обработки случаев  `<!--<script>`

# 3.0.0

Выпилил весь yate-код из apiary

Переписал весь системный тест (systest) - обновил снэпшоты

Исправил ошибку ts при сборке apiary, падало на export = invariant

Исправил ошибку с flow связанную с отсутсвием в .flowconfig строки: suppress_comment=\\(.\\|\n\\)*\\$ExpectError

Добавил запуск системного теста в jest.config

Добавил заглушки в системном тесте для apiary-marker-id и total size, которые зависят
от порядка запуска тестов

Теперь можно запускать тесты командой npm run test:jest, или напрямую из файла systest/index.spec.ts

Поправил README.md - убрал упоминания yate, исправил ссылки

### Usage

Без изменений

### Migration

Без yate-виджетов в зависымых проектах

### Updates

  * `@yandex-market/invariant`: [0.4.0](../invariant/changelog.md#040) (was [0.3.5](../invariant/changelog.md#035))

# 2.0.8

Обновление зависимостей

# 2.0.7

Игнорим node_modules-prod для автотестов

### Updates

  * `@yandex-market/error`: [1.4.5](../error/changelog.md#145) (was [1.4.4](../error/changelog.md#144))
  * `@yandex-market/invariant`: [0.3.5](../invariant/changelog.md#035) (was [0.3.4](../invariant/changelog.md#034))

# 2.0.6

Нативная зависимость от yate

# 2.0.5

Нативная зависимость от yate

# 2.0.4

Фиксы тестов

### Updates

  * `@yandex-market/error`: [1.4.4](../error/changelog.md#144) (was [1.4.3](../error/changelog.md#143))
  * `@yandex-market/invariant`: [0.3.4](../invariant/changelog.md#034) (was [0.3.3](../invariant/changelog.md#033))

# 2.0.3

Обновление версий зависимостей

# 2.0.2

Поправил ченжлог

### Updates

  * `@yandex-market/error`: [1.4.3](../error/changelog.md#143) (was [1.4.2](../error/changelog.md#142))
  * `@yandex-market/invariant`: [0.3.3](../invariant/changelog.md#033) (was [0.3.2](../invariant/changelog.md#032))

# 2.0.1

Переезд в монорепу

### Updates

  * `@yandex-market/error`: [1.4.2](../error/changelog.md#142) (was [1.4.1](../error/changelog.md#141))
  * `@yandex-market/invariant`: [0.3.2](../invariant/changelog.md#032) (was [0.3.1](../invariant/changelog.md#031))
  * `eslint-plugin-stout`: [1.0.3](../../tools/eslint-plugin-stout/changelog.md#103) (was [1.0.2](../../tools/eslint-plugin-stout/changelog.md#102))
