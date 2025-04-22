# FAQ по Лего

## Почему нет документации по React-компонентам?

Черновой вариант: https://lego.yandex-team.ru/lego-on-react/

На беловой решили не тратиться, а в новой реализации компонентов на TypeScript хотим срезать углы и генерировать документацию из кода, потому что так дешевле.

## Почему не получается ввести текст в TextInput (lego-on-react)?

`TextInput` - stateless-компонент.
`text` необходимо держать в `state` и обновлять через `onChange`.

[Пример в песочнице](https://nda.ya.ru/3UWTVx)

## Почему не закрывается Popup (lego-on-react), хотя ему передан `autoclosable`?

Необходимо передать обработчик `onOutsideClick`.

[Пример в песочнице](https://nda.ya.ru/3UWTVy)

## Можно ли TextInput добавить маску?

В Лего такой возможности нет, но вы можете использовать сторонние библиотеки с нашими компонентами

[Пример с react-text-mask](https://lego-staging.dev.yandex-team.ru/islands/dev/desktop.examples/textinput/react/)

## Есть ли в Лего Datepicker?

Готового нет. Компонент не самый простой, но явно нужный.

Задачи в трекере, связанные с календарем:
[ISL-3575](https://st.yandex-team.ru/ISL-3575)
[ISL-3542](https://st.yandex-team.ru/ISL-3542)
[ISL-3580](https://st.yandex-team.ru/ISL-3580)
[ISL-3877](https://st.yandex-team.ru/ISL-3877)

Есть, к примеру, вот такой вариант стилизации react-datepicker под контролы Яндекса: [https://github.yandex-team.ru/testpalm/testpalm-www/tree/master/src/blocks/DatePicker](https://github.yandex-team.ru/testpalm/testpalm-www/tree/master/src/blocks/DatePicker)

## Как контрибьютить код?

[Contribution Guideline](../CONTRIBUTING.md)

## Что делать, если нет необходимых PropTypes или они написаны неправильно?

Напишите нам об этом или принесите PR с вашими [исправлениями](../CONTRIBUTING.md)

## Есть в lego-on-react компонент как suggest, только чтобы не ходил в ручку, а по данным из массива подсказывал?

`TextInput_suggest_yes`

[Пример в песочнице](https://nda.ya.ru/3UWaKC)

## Как правильно в Tooltip (lego-on-react) передать ref, чтобы он открылся на первой же отрисовке?

В реакте `ref` привязывается асинхронно и после рендера элемента.
Когда тот компонент, в котором tooltip лежит, отрисовывается - ref, который передается в tooltip, равен undefined.
Сейчас в `anchor` можно передать функцию, которая будет возвращать ссылку на нужный узел.

`<Tooltip anchor={() => this.anchorRef}>`

## Можно ли как-то заставить кнопку моргать при `progress=true`, а не просто делать недоступной?

[Пример в песочнице](https://nda.ya.ru/3UVVeD)


## Как построить дерево зависимостей ENB? Приезжает блок bemhtml на клиент

Нужно пройтись по связкам `tech: 'js', {should,must} Deps: { tech: 'bemhtml' }` в deps.js, по ним `ENB` определяет, что нужно включить в `deps-by-tech`, и построить обратные зависимости, примерно как в `gather-reverse-deps`.

Можно начать примерно с `find . -name '*.deps.js' | xargs -n 500 grep -E 'tech:.*bemhtml'`, получить deps-by-tech связки, и дальше посмотреть цепочку от искомого блока до тех, кто его зовет

## Как в свойство iconLeft/iconRight блока Link прокинуть свою иконку?

[Пример в песочнице](https://nda.ya.ru/3UVfMw)

## Как посмотреть лог изменений?

На нашем сайте в [примечаниях к релизу](https://lego.yandex-team.ru/libs/islands/v5.27.0/notes/)

## Есть ли готовый компонент для работы с `<input type="file">`?

`Attach`

## Что делать с ошибкой 404 при установке npm пакетов, которые начинаю с @?

Добавить в .npmrc  registry: `@<your-value>:registry=https://registry.npmjs.org/`

## Как показать дизайнеру дизайн компонентов, которые есть в lego-on-react?

[Showcase](https://lego-staging.dev.yandex-team.ru/islands/dev/desktop.examples/showcase/new/new.html)
[Документация](https://lego.yandex-team.ru/libs/islands/v5.27.0/desktop/button2)
[Песочница](https://lego.yandex-team.ru/brickbox/)

## Как в lego-on-react для компонента `Button` добавить иконку?

[Пример в песочнице](https://nda.ya.ru/3UVxJL)

## В Select из lego-on-react  не вызывается onChange

Нужно ещё указать тип селекта: `radio` либо `radiocheck`

## Что делать, если хочется свой блок принести в Лего?

Внимательно ознакомиться с [условиями добавления](https://lego.yandex-team.ru/doc/guidelines/new-improvements-and-blocks/#Условия-добавления-и-поддержки-блоков-в-Лего)

## Как управлять границами Button2 ?

Нужно использовать модификатор  `pin`

[Примеры](https://lego-staging.dev.yandex-team.ru/islands/dev/desktop.examples/button2/all/all.html#Pin)

## Как показать аватары для @yandex-team.ru в User-* компонентах?

[Пример в песочнице](https://nda.ya.ru/3UWFom)

## Подключил в проект реактовский колокольчик. При отправке уведомлений колокольчик у нас не загорается, а на Серпе загорается. Не знаете почему такое происходит? Может колокольчик надо настроить, чтобы загорался?

Нужно импортировать [стили для тикера](https://github.yandex-team.ru/search-interfaces/frontend/blob/master/projects/lego/packages/notifier/common.blocks/notifier/__ticker/notifier__ticker.css)

## Какой у вас релизный flow? Как вы собираете список задач, который покатится, как создаете релизную задачу, как закрываете все задачи, которые выкатились, и т д?

У нас есть [инструкция](https://github.yandex-team.ru/search-interfaces/frontend/tree/master/projects/lego/guidelinesrelease.md)

Если коротко — у нас есть линтеры, которые проверяют, что в задачах проставлены компоненты (мажор/минор/патч), и если это минор-мажор, то должна быть документация к релизу в специальном файле.

Потом `iver` собирает все PR с последнего релиза, соотносит их с задачами в Трекере, из них получает компоненты и считает новую версию, из документов собирает релизный документ

## Как найти и подключить шрифты (Font)?

Из библиотеки `lego-on-react` был удален компонент `Font` из-за проблем с итоговым размером сборки, теперь для использования шрифтов необходимо загружать их со статики, например:

https://yastatic.net/s3/home/fonts/ys/1/text-regular.woff2
https://yastatic.net/s3/home/fonts/ys/1/text-medium.woff2
https://yastatic.net/s3/home/fonts/ys/1/text-bold.woff2

Список доступных шрифтов со ссылками на статику можно посмотреть на странице [примеров](https://lego.yandex-team.ru/__example/islands/v5.27.0/desktop.examples/i-font/all/all.html#Шрифты)
Пользователей  `islands` на  `i-bem/bem-xjst` изменения в коде React-компонент не касаются.

## Как установить текст по умолчанию в Select?

Надо передать нужное значение в параметр:
- React: `placeholder="Переданный текст"` [Пример в песочнице](https://nda.ya.ru/3UWk9m)
- i-bem: `text="Переданный текст"` [Пример в песочнице](https://nda.ya.ru/3UWkE5)

Если `type='radio'` - то текст по умолчанию не будет подставляться, потому что `radio` позволяет выбрать только один пункт. Если пункт не выбран, то по умолчанию выбирается первое значение из списка.

В будущем объединим их в одно свойство, чтобы API было одинаковым: https://st.yandex-team.ru/ISL-3364

## Что сделать, чтобы в RadioButton текст не выходил за границы?

Необходимо передать `freeWidth`.

[Пример в песочнице](https://nda.ya.ru/3UXCqW)

## Что сделать, чтобы User2 корректно работал на iOS?

Блок нужно использовать внутри блока `b-page`, так как `b-page` содержит стили для корректной работы `user2`, либо необходимо вручную добавить стили из `b-page` для `body`, если не проставить на body стили `cursor:pointer` , то никаких событий не будет и клики вне попапа никак обрабатываться не будут.

## Что делать, если не нашли ответа на свой вопрос?

Задавайте свои вопросы в рассылку или в чат.

## Странный визуальный баг в Safari, который не воспроизводится в Песочнице

Это может быть багом рендеринга, в Safari такое встречается достаточно часто (поэтому будьте осторожны, если используете, например, CSS Custom Properties).
Чаще всего это можно полечить, добавив проблемному элементу `transform: translateZ(0)` (т.е. вынесением отрисовки на отдельный слой).
Такие баги обычно проявляются для определенной специфической совокупности стилей.

Например, проблема множественных курсоров в `textarea`, когда в `iframe` лежит элемент с `position: fixed`, внутри него - контейнер с `display: flex`, шрифт задается с помощью CSS Custom Properties, а у `textarea` есть `border` и `outline` (если убрать любой из этих стилей, все будет хорошо; открывать в Safari): https://jsbin.com/jiyezucika/1/edit?html,css,output

## trendbox-таска в CI упала не по моей вине, но при перезапуске сразу падает снова

Пожалуйста, убедить, что вы правильно выставили `OWNER`:

![](https://jing.yandex-team.ru/files/koreil/Task_379649733_TRENDBOX_CI_JOB_BETA_2019-02-16_11-01-03.png)

Для `trendbox`-тасок это должен быть `LEGO_TRENDBOX_CI`, для `sandbox`-тасок - `SANDBOX_CI_SEARCH_INTERFACES`.

[Обратная связь](../README.md#Обратная-связь)
