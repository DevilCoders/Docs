# Бункер

[Бункер](https://wiki.yandex-team.ru/verstka/tools/bunker/) — это хранилище разных статических данных (обычно в формате JSON), которые можно редактировать динамически людьми далекими от разработки (менеджеры, маркетологи и т.д.).
Он может использоваться, к примеру, для хранения тестов для различных промо-страниц, ссылок на изображения, небольших таблиц, данные в которых могут нуждаться в периодическом обновлении со стороны менеджеров. В этом случае бункер можно воспринимать как некое подобие админки для контент-менеджеров. То есть при его использовании всегда лучше предусматривать возможность ошибки в данных.

[Раздел Авто.ру в Бункере](https://bunker.yandex-team.ru/auto_ru?view=raw)

## Запрос прав

![Запрос прав](https://jing.yandex-team.ru/files/alivander/Снимок%20экрана%202019-07-16%20в%2022.15.52.png)

Права на редактирование и публикацию выдаются через [IDM](https://idm.yandex-team.ru/user/alivander/roles#rf=1,rf-role=EfBE0mSs#bunker/auto_ru/*/store;;;,rf-expanded=EfBE0mSs,f-status=all,sort-by=-updated). Если по ссылке параметры не подтянулись автоматически, нужно выбрать проект `auto_ru`, затем выбрать "Выбор узла завершен", а затем уже уровень доступа (отдельно "Редактирование данных" и "Публикация узлов").

В подавляющем большинстве случаев вам достаточно получить права только на редактирование.

В dev и testing используется последняя **отредактированная** версия, а для прода – последняя **опубликованная**.
Т.о. при редактировании (создании новых узлов, сохранении изменений) данные меняются сразу только в dev и testing, а уже публикация меняет их в production.

Чтобы подхватить новые данные бункера в деве или тестинге, надо просто рестартануть приложение:
```sh
make restart
```

В проде данные обновляются сами, таймаут указан в `process.env.BUNKER_REFRESH`.

## Редактируем нужные данные

Редактируем/создаем соответствующие узлы в [Бункере](https://bunker.yandex-team.ru/auto_ru/common/cert_staff?view=raw)

![Редактирование](https://jing.yandex-team.ru/files/alivander/Снимок%20экрана%202019-07-16%20в%2022.19.50.png)

Для dev/testing жмем "Сохранить".
Для прода, хорошо подумав, "Опубликовать". Лучше оставить публикацию ответственным лицам :)
Чтобы о публикации не забыли и в проде код, завязанный на данные из бункера, не упал, обязательно приложите ссылку на данные в бункер в описание задачи, укажите что она нуждается в публикации и добавьте в название таска тег [ bunker ].

## Как использовать в серверном коде

В priv'ах, в preparer'ах и т.д.:

```js
const getBunkerDict = require('auto-core/lib/util/getBunkerDict');

const certStaff = getBunkerDict('common/cert_staff');
//  То же самое, но с явно заданной группой.
//  const certStaff = getBunkerDict('common/cert_staff', 'auto_ru');
```

## Как использовать в связке `descript/React`

В пейджовом descript-блоке добавляем:

```js
const de = require('descript2');
const getBunkerDict = require('auto-core/lib/util/getBunkerDict');

module.exports = {
    ...

    bunker: de.func({
        block: () => ({
            'common/cert_staff': getBunkerDict('common/cert_staff'),
            ...
        }),
    }),

    ...

};
```

Убеждаемся, что подключен нужный reducer:

```js
module.exports = createReducer({
    ...
    bunker: require('auto-core/react/dataDomain/bunker/reducer'),
    ...
});
```

В компоненте получаем нужные данные из стора:

```js
const getBunkerNodeSelector = require('auto-core/react/dataDomain/bunker/selectors/getNode');

function mapStateToProps(state) {
    return {
        certStaff: getBunkerNodeSelector(state, 'common/cert_staff'),
        ...
    };
};
```
