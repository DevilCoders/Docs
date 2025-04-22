# AJAX

## Загрузка дополнительных данных

По умолчанию любой адаптер будет отвечать на ajax-запросы пустым ответом. Для того чтобы переопределить такое поведение нужно в адаптере реализовать два метода: `getSnippetForAjax` и `ajax`.

Допустим, у нас есть адаптер AdapterFeatureName и мы хотим, чтобы при клике на кнопку, в фиче что-то обновилось. Для этого реализуем необходимые методы — см. [LearnSerpAjax.server.ts](./features/LearnSerpAjax/LearnSerpAjax.server.ts)

## Ajax-запрос из react-блока

Результат можно увидеть по адресу [search/?foreverdata=438546217&exp_flags=learn_serp_bem-ajax-react](https://yandex.ru/search/?foreverdata=438546217&exp_flags=learn_serp_bem-ajax-react).

1. В React мире для отправки ajax-запросов нужно подготовить бандлы вызовом функции `setupAjaxUpdater` — см. [LearnSerpAjax_react.server.tsx](./features/LearnSerpAjax/_react/LearnSerpAjax_react.server.tsx)

2. В компоненте делаем ajax-запрос к адаптеру через вызов `ajaxUpdate` — см. [ReactReason.tsx](./components/ReactReason/ReactReason.tsx)

**Внимание:** имя адаптера и его subtype нужно указывать так как он задекларирован в `src/features/.registry`, (либо в `src/experiments/.registry`)
например колдунщик картинок `adapter: 'images'` с маленькой буквы, а `adapter: 'LearnSerpAjax'` с большой буквы.

## Ajax-запрос из конструкторского блока (в ts-адаптер)

Рабочий пример можно увидеть по адресу [search/?foreverdata=609826886&exp_flags=learn_serp_bem-ajax-react](https://yandex.ru/search/?foreverdata=609826886&exp_flags=learn_serp_bem-ajax-react)

1. Для того блока которому нужно обновление вызвать "supply__ajax-updater" и создать элемент ajax — см. [react-reason.priv.js](../../../experiments/learn_serp_bem-ajax-react/blocks-common/react-reason/react-reason.priv.js)

2. В клиентском коде этого блока сгенерировать событие `ajax-update` — см. [react-reason.js](../../../experiments/learn_serp_bem-ajax-react/blocks-common/react-reason/react-reason.js)

## Загрузка React фичей

Иногда нет возможности переписать фичу на react, но какие-то большие части фичи очень хочется переписать.

Пример можно посмотреть по адресу [search?foreverdata=3781239561&exp_flags=learn_serp_bem-ajax-react](https://yandex.ru/search?foreverdata=3781239561&exp_flags=learn_serp_bem-ajax-react). Надо нажать на кнопку "Хочу видеокурс по React".

1. Реализовать адаптер, который будет отдавать часть фичи — см. [LearnSerpAjaxPlayer.server.tsx)](./features/LearnSerpAjaxPlayer/LearnSerpAjaxPlayer.server.tsx)
2. Реализовать блок-загрузчик, в котором нужно добавить загрузчик "i-react-ajax-update" — см. [react-reason.priv.js](../../../experiments/learn_serp_bem-ajax-react/blocks-common/react-reason/react-reason.priv.js)

3. В клиентской реализации блока-загрузчика вызвать загрузку React через `BEM.channel('i-react-ajax-update').trigger('ajax:render', {...})` — см. [react-reason.js](../../../experiments/learn_serp_bem-ajax-react/blocks-common/react-reason/react-reason.js)
