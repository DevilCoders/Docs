# Разработка в `b2b-components`

## Настройка окружения

### Установка

- Установить зависимости для разработки `b2b-components` можно следующим образом:

  ```sh
  npm install
  ```

  Если используется `veendor`:

  ```sh
  veendor install
  ```

- Однако у `b2b-components` также есть `peer`-зависимости, которые нужно ставить отдельно с помощью команды:

  ```sh
  npm run bootstrap
  ```

- Таким образом установить сразу все можно так:

  ```sh
  npm install && npm run bootstrap
  ```

### Commit git hook

С установкой `dev`-зависимостей будет также установлен гит-хук, который выполнит следующие проверки на коммит:
  - проверит codestyle (eslint (js, flowtype), stylelint (css)). Проверяться будет только **измененный/добавленный** код;
  - проверит типизацию (flow). Проверяться будет **весь проект**.

## Разработка

### Styleguide

Каждый компонент должен быть отражен и описан в стайлгайде с примерами. Для этого мы используем [styleguidist](https://react-styleguidist.js.org/). Основные моменты:
- для того, чтобы поднять дев-сервер стайлгайда (с HMR), есть команда:

  ```sh
  npm run styleguide
  ```
- у каждого компонента есть `Readme.md` с его описанием и примерами работы. Почитать можно [тут](https://react-styleguidist.js.org/docs/documenting.html#writing-code-examples)
- в примерах должны быть показаны основные возможности и состояния компонента
- иногда компоненту требуется `state`. И если `initialState/setState` из документации не хватает, или же этот код дублируется/усложняется из примера в пример, то эту логику можно вынести в `.styleguidist/ctx.js`. Например:

  Описание контекста компонента:
  ```js
  // Контекст получает следующие опции: `state` из контекста примера, функцию `setState` из контекста примера, а также `name` - название данных компонента в стейте для данного примера
  export const DatePicker = ({state, setState, name = 'datePicker'}) => ({
    // создание initialState
    get initialState() {
        return {[name]: new Date()};
    },

    // получение значения в стейте
    get value() {
        return state[name];
    },

    // функция для изменения стейта
    onChange: value => setState({[name]: value}),
  });
  ```

  Пример использования в `Readme.md`:
  ```js
  // реквайрим нужный нам Компонент, если он не доступен в обычном скоупе
  const {DatePickerDropdown} = require('../Datepicker');

  // создаем контекст для DatePicker
  const {datePicker} = ctx.DatePicker({state, setState});

  // создаем контекст для Select
  const select = ctx.Select({state, setState});

  // мержим полученные initialState
  initialState = Object.assign({}, datePicker.initialState, select.initialState);

  // используем
  <section>
    <DatePickerDropdown value={datePicker.value} onChange={datePicker.onChange} />

    <Select value={select.value} onChange={select.onChange}>
        {select.Options}
    </Select>
  </section>

  ```
- также в `ctx` можно описать общие хелперы, которые могут использоваться во всех примерах

### В стороннем проекте

Если необходимо вносить изменения в `b2b-components`, при этом не меняя собственный процесс разработки (с использованием HMR, линтинга и т.д.), то стоит удостовериться, что пройдены следующие этапы:

1) Установить в рабочем проекте обычные зависимости
2) Установить в b2b обычные и peer зависимости (см. [Установка](#Установка))
3) Сделать в проекте симлинк на b2b:

    ```sh
    rm -rf node_modules/@yandex-market/b2b-components
    ```

    ```sh
    ln -s /absolute-path-to/b2b-components/ node_modules/@yandex-market/
    ```
4) Убить процесс Flow/перезапустить флоу-сервер (он мог остаться от предыдущего запуска линтинга).
5) Запустить сборку в проекте (например, в `partnernode` с помощью `npm run dev`)

При этом важно удостовериться, что в конфиге вебпака проекта точно указаны модули, которые должны использоваться в сборке (`resolve.modules`), и не используются модули из `b2b-components` соответственно.

## Релиз

Перед релизом из локальной копии необходимо убедиться, что:
- необходимые PR-ы вмержены в мастер (удобно вмержить через интерфейс GitHub, а затем сделать `git pull` для подтягивания изменений локально);
- локально мы находимся в ветке `master`;
- установлены зависимости (`npm install && npm run bootstrap`);
- установлен пакет `github_changelog_generator` ([как поставить](#changelogmd));
- прогон eslint-а не показывает ошибок `eslint . --ignore-pattern !.*.js` (Если показывает, но в смерженных PR-ах проблем не было, локально в мастере запускем проверку с флагом `--fix`, коммитим изменения и пушим прямо в `master` удаленного репозитория);
- в корень локальной копии добавлен файл `.github_changelog_generator` ([как добавить](#changelogmd));
- в терминале установлена восьмая `node.js` (`nvm use 8`);
- есть права мейнтейнера на публикацию версии в npm ([как получить права](#npm-доступы)).

Версии определяем по [semver](https://semver.org/).

Для релиза новой версии необходимо выполнить команду:

```sh
npm version {major|minor|patch}
```

Если тесты и линтинг будут пройдены успешно, то
- обновится CHANGELOG.md с релизной версией ([подробнее](#changelogmd))
- обновится версия `package.json`
- новая версия стайлгайда задеплоится на `gh-pages`
- новая версия компонентов будет запушена с релизным тэгом на гитхаб
- новый пакет будет выложен в `npm`

В случае, если нужны ручные изменения в `CHANGELOG.md` (или где-то еще), то можно запустить релиз с флагом `--w` (wait):

```sh
npm version {major|minor|patch} --w
```

Тогда после генерации ченджлога будет пауза, когда возможно внести собственные правки (или сделать что-нибудь еще), после чего ввести `y` и продолжить релиз, либо отменить, если что-то пошло не так.

### CHANGELOG.md

Для автоматического обновления `CHANGELOG.md` используется [github-changelog-generator](https://github.com/skywinder/github-changelog-generator) версии `>= 1.15.0-rc`.

Для установки можно выполнить:

```sh
gem install github_changelog_generator -v 1.15.0-rc
```

Для установки понадобится версия Ruby >= 2.5.0. Удобно поставить версию через [rvm](https://rvm.io) (аналог nvm);

```sh
curl -sSL https://get.rvm.io | bash -s stable
source /Users/_НАЗВАНИЕ_ПОЛЬЗОВАТЕЛЯ_/.rvm/scripts/rvm
rvm install 2.5.0
rvm use 2.5.0
```

Также github-api имеет лимит для запросов без токена. Соответственно для того, чтобы `changelog` сформировался верно, нужно указать свой токен в конфиге генератора (~~бесплатно и без смс~~ получить его можно [тут](https://github.yandex-team.ru/settings/tokens))

В итоге в корне проекта нужно добавить файл `.github_changelog_generator` со следующим содержимым:

```md
token={полученный github-токен}
github-site=https://github.yandex-team.ru/
github-api=https://github.yandex-team.ru/api/v3
user=market
project=b2b-components
```

### npm доступы 

Для получения прав на публикацию версии npm нужно:
- взять существующего или создать нового юзера npm на [официальном сайте npm](https://www.npmjs.com);
- добавить пользователя в репозиторий пакетов npm Яндекса и залогиниться через терминал (http://npm.yandex-team.ru);
```sh
npm adduser --registry=http://npm.yandex-team.ru
npm login --registry=http://npm.yandex-team.ru
```
- попросить мейнтейнера (например, Артура Кенжаева) выдать права пользователю на публикацию новой версии.

