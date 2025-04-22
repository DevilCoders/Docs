### Интро
- [порядок разработки продукта внешними силами](https://wiki.yandex-team.ru/morda/ui/external-dev/)
- [общий ликбез по разработке фронтенда](https://wiki.yandex-team.ru/morda/ui/likbez/)

### Структура проекта
- `divcards` — код дивных блоков для ПП
- `frontend-node` — код node.js сервиса
- `js_libs` — библиотека утилит
- `common` — уровень общих блоков
   - `blocks` — общие блоки для всех типов страницы
   - `blocks-desktop` — для десктопных страниц
   - `blocks-touch` — для тачевых страниц
- `touch` — уровень тачевых страницы
   - `blocks/touch`, `blocks/touch-redesign` — блоки основной тачевой страницы
   - `blocks/gramps` — дедуля
   - `blocks/blocks-mini` — общие блоки для mini-страниц (spok, yaru, world)
   - `blocks/spok` — семейство страниц на региональных доменах, например, https://yandex.az/
   - `blocks/yaru` — тачевое https://ya.ru/
- `white`— уровень десктопных страниц
  - `blocks/bender-*` — блоки основной десктопной страницы
  - `blocks/gramps` — дедуля
  - `blocks/newtab3` — страница на NTP Хрома
  - `blocks/spok*` — семейство страниц на региональных доменах, например, https://yandex.az/
  - `blocks/yaru` — десктопное https://ya.ru/
  - `blocks/yabro-*` — страница на NTP Я.Браузера
- `tv` — уровень страницы для ТВ
- `pda`, `wap`, `yaru`, `yabro` — уровни страниц для старых клиентов

### Кодовая база
- соблюдение code style — код командой создается так, будто его пишет один человек:
  - консистентное устройство компонентов
  - именования
  - но могут быть исключения
- typescript first: `.tsx` на сервере, `.ts` на клиенте
- не добавлять новые `*.view.html` шаблоны
- использование танкера для текстовых токенов
- расширение [CSP в компонентах](https://wiki.yandex-team.ru/morda/ui/likbez/#csp)
- следование логике уровня переопределений:
  - на уровне `common` нельзя импортировать код с любых уровней, кроме `common`
  - на уровне `desktop` нельзя импортировать код с уровней `touch`, но можно с уровней `common` и `desktop` и т.д. Нарушение этого правила может повлечь за собой неожиданные эффекты и баги
- юнит тесты: [hermione](https://wiki.yandex-team.ru/morda/ui/tests/#hermione) (веб, ПП), [снепшоты](https://wiki.yandex-team.ru/morda/ui/tests/#unit-testynaviews) (веб)
- [тесты на утилиты](https://github.yandex-team.ru/morda/main/tree/dev/tmpl/js_libs/ts/utils/tests)
- фичи за кликом по возможность уносить за [динамический импорт](https://wiki.yandex-team.ru/morda/ui/dynamic-imports/)
- новые фичи — за [аб-флагами](https://wiki.yandex-team.ru/morda/ui/likbez/#exp).

### Надежность
- логирование ошибок
- [отключаемость](https://wiki.yandex-team.ru/morda/ui/likbez/#options/opcii)


### Качество компонента
- продуктовое логирование, проверять с [дежурным аналитиком](https://abc.yandex-team.ru/services/home/duty/?role=2290)
- поддержка темной темы
- адаптация под ландшафтный режим
- ховеры на десктопах
- зоны клика
- доступность с клавиатуры и программ голосового чтения
- адаптация или понятная стратегия скрытия про ресайзе.
- использование относительных ``line-height`` при работе с текстом

### Процесс разработки
- техническое обсуждение накануне разработки (желательно, в формате встречи с руководителями групп [фронтенда](https://staff.yandex-team.ru/departments/yandex_distproducts_morda_social/) и [бекенда](https://staff.yandex-team.ru/departments/yandex_distproducts_morda_passport_dep20617)).
- [порядок решения задачи](https://wiki.yandex-team.ru/Morda/workflow/), tldr:
   - PR и обязательные апрувы для передачи в тестирование
   - план тестирования, контроль качества компонента со стороны тестирования морды
   - мерж в dev после прохождения тестирования

### Советы и прошлый опыт
https://st.yandex-team.ru/HOME-69335#60c9c29859923b23a1d529ea
