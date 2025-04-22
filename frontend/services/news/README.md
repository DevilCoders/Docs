# Neo
React-фреймворк для разработки веб-сервисов. Поддерживает server-side и client-side rendering.
Основной акцент сделан на максимально полное описание TypeScript-типов и передаче данных через React Context.

## Запуск
Для начала запускаем в директории `frontend`:
`nvm use`, `npm ci` и `npx lerna bootstrap --scope @yandex-int/news --scope @yandex-neo/core --scope @yandex-neo/configs --scope @yandex-neo/mg --scope @yandex-neo/tools --scope @yandex-neo/eslint-plugin`

`npm run dev` запустит сборку в dev-режиме и dev-сервер
`npm run build` запустит сборку в режиме production
`npm run start` запустит проект (используется после команды npm run build)
`npm run lint` запустит линтеры
`npm run unit` запустит unit-тесты

## Контексты (React Context)
Общие контексты лежат в `neo/contexts`.
Все контексты доступны в любом компоненте, а так же рекомендуется всегда пробрасывать первым параметром serverCtx в server-side функции в директориях `<service>/src/lib`.

Пример:
```
import { useServerCtx } from 'neo/hooks/contexts/ServerCtx';
const serverCtx = useServerCtx<IServerCtx>();
```

##### ApplicationCtx
Контекст для общей информации о текущем запросе и приложении. Содержит информацию о текущем сервисе, платформе, странице.
*Доступен на сервере и клиенте.*

##### DataSourceCtx
Через dataSource прокидываются данные с сервера на клиент. Для отдельных страниц необходимо описать интерфейсы dataSource в директории наподобие `src/types/news/datasource/pages/IDataSourceFeed.phone.ts`. Все специфичные для страницы данные должны быть в dataSource.
*Доступен на сервере и клиенте.*

##### ServerCtx
Служит для хранения и проброса данных на server-side во время обработки запроса. Содержит информацию о http-заголовках, get-параметрах, куках и дополнительную служебную информацию.
*Доступен только на сервере.*

## Эксперименты
см. [Документацию в neo-core](https://a.yandex-team.ru/arc/trunk/arcadia/frontend/packages/neo-core/docs/experiments.md)

## Классы
Используется пакет [@bem-react/classname](https://github.com/bem/bem-react/tree/master/packages/classname).
В директориях `<service>/src/lib` должны лежать `cn.ts` файлы с инициализацией соответстующего неймспейса, которые должны экспортировать ClassNameInitilizer (Initilizer блеать). [Пример](https://github.yandex-team.ru/search-interfaces/frontend/blob/master/services/news/src/neo/lib/cn.ts).
В директории с компонентом рекомендуется создавать файл `<Компонент>.cn.ts`, который должен подключать соответствующий `cn.ts` файл из директории `src/<service>/lib`. [Пример](https://github.yandex-team.ru/search-interfaces/frontend/blob/master/services/news/src/neo/components/App/App.cn.ts).
Для того, чтобы в коде смиксовать несколько классов, используется второй опциональный аргумент (всегда массив). Пример:
```tsx
import { cls } from './App.cn';

export function App(props: IProps) {
  return <div className={cls(null, [props.className])} />;
}
```

## Использование svg (в *.tsx файлах)
Импортим
`import NeoLogo from 'neo/assets/neo.svg';`
вставляем
`<NeoLogo />`
можно использовать любые атрибуты, которые применимы к svg
`<NeoLogo width="20" height="20" />`

## Использование png, jp(e)g, ico, (svg в *.scss файлах)
- В файлах `*.scss` при вставке картинки в качестве background указываем локальный путь к ассету.
Если её размер меньше 8Кб, то она заинлайнится в `base64`, иначе зафризится на `frontend.s3.static`


- В файлах `*.tsx` импортим   
`import pathToImage from 'neo/assets/imageName.png';`   
И используем `pathToImage` в качестве пути до картинки, который заменится в конечной сборке на `https://frontend.s3.static/news/_/imageHash.png` 

## Правила именования компонентов в директории <service>/src/components
#### Общий вид
<приложение>/components/<компонент>/<компонент>.<платформа>.tsx

Пример:
*neo/components/Layout/Layout.desktop.tsx*

#### Модификаторы
<приложение>/components/<компонент>/\_<модификатор>/<компонент>\_<модификатор>.<платформа>.tsx

Примеры:
*neo/components/Layout/\_Big/Layout_Big.phone.tsx*
*neo/components/Layout/\_Type/Layout_Type_Event.phone.tsx*

#### Элементы
<приложение>/components/<компонент>/\_\_<элемент>/<компонент>\_\_<элемент>.<платформа>.tsx

Пример:
*neo/components/Layout/\_\_Item/Layout\_\_Item.desktop.tsx*

#### Модификаторы элементов
<приложение>/components/<компонент>/\_\_<элемент>/<компонент>\_\_<элемент>\_<модификатор>.<платформа>.tsx

Примеры:
*neo/components/Layout/\_\_Item/Layout\_\_Item_Big.phone.tsx*
*neo/components/Layout/\_\_Item/Layout\_\_Item\_Type\_Event.phone.tsx*

### Название экспортируемого компонента должно совпадать с названием файла, но без символов нижнего подчёркивания, платформы и расширения
Пример:
*Файл neo/components/Layout/\_\_Item/Layout\_\_Item\_Type\_Event.phone.tsx*
*Экспортируемый компонент LayoutItemTypeEvent*

## Баобаб

[Документация расположена здесь](https://a.yandex-team.ru/arc/trunk/arcadia/frontend/packages/neo-core/src/lib/baobab/README.md)

## Дополнительная информация

## production-сборка и переменные окружения
#### NODE_ENV отвечает за тип собираемых бандлов
Возможные значения: production и development. По умолчанию development.

#### YENV отвечает за пути к статике
Возможные значения: production, testing и development. По умолчанию development. production и testing значения должны использоваться только с `NODE_ENV=production`.

`NODE_ENV=production YENV=production npm run ci:build` Помимо сборки production-бандлов подменяет в них пути до статики на production значения
`NODE_ENV=production YENV=testing npm run ci:build` Помимо сборки production-бандлов подменяет в них пути до статики на testing значения

## Storybook

`npm run storybook`

## Тестирование

### Unit (Jest)

`npm run unit <путь к тесту>` - запуск теста
`npm run unit -- <путь к тесту> -u` - переснять snapshot'ы

### Hermione (Storybook)

```text
src/components/Block

├── __tests__
│  ├── Block.phone.hermione.js — Hermione тесты для тача
│  ├── Block.desktop.hermione.js — Hermione тесты для десктопа
│  └── Block.test.js — Unit тесты
├── Block.tsx
└── Block.story.tsx - Сторибук
```
```ts
Пример

describe('Цитата', () => {
  it('должна отображаться корректно', function() {
    return this.browser
      .openComponent('quote', 'default')
      .assertView('quote', '.mg-quote');
  });
});
```

`npm run hermione:storybook:build` - Собрать сторибук

`npm run hermione:gui -- <путь к тесту> --retry 0 -a` - Запустить тесты

`npm run hermione:gui -- --from=https://proxy.sandbox.yandex-team.ru/<id>/index.html` - Запустить тесты из html-отчёта, когда обнаружились отклонения. Чтобы узнать id, нажми на view source

### Hermione (Features)

Тесты только для тача или десктопа
*.phone.hermione.js
*.desktop.hermione.js


```text
src/components/Block

├── features
│  ├── news - Сервис
│  │  ├── index - Название фичи
│  │  │  ├── index.phone.hermione.js — Hermione тесты
│  │  │  ├── index.phone.testpalm.js — Тестпалм
│  │  ├── e2e - e2e тесты
│  │  │  ├── index - Название фичи
│  │  │  │  ├── index.phone.hermione.js — Hermione тесты
│  │  │  │  ├── index.phone.testpalm.js — Тестпалм


```

```ts
Пример

describe('Сервис Я.Новостей', () => {
  it('открывается главная рубрика', function() {
    return this.browser
      .yaOpenUrl('/news')
      .assertView('plain', 'body');
  });
});
```

`npm run build` - Собрать

`npm run hermione:gui -- <путь к тесту> --play --retry 0 -a` - Запустить тесты с уже сформированными дампами в test-data (см. `--play`)

`npm run hermione:gui -- --from=https://proxy.sandbox.yandex-team.ru/<id>/index.html` - Запустить тесты из html-отчёта, когда обнаружились отклонения. Чтобы узнать id, нажми на view source

Для тестирования кейсов, где нужен авторизованный пользователь, используется hermione-плагин [`hermione-auth-on-record-commands`](https://github.yandex-team.ru/search-interfaces/infratest/tree/master/packages/hermione-auth-on-record-commands#команды)
Если нужно сохранить дамп за логином, воспользуйтесь командами:
- `authOnRecord(login, options)` - следует использовать в тестах, где не меняется состояние пользователя (нам важно именно наличие авторизации и больше ничего)
- `authAnyOnRecord(groupPrefix, options)` - следует использовать в тестах, где состояние пользователя изменяется и по этой причине параллельное снятие дампов в нескольких браузерах может быть затруднено

Обратите внимание на рекомендацию плагина переиспользовать аккаунты между тестами:
текущие ограничения TUS на общее количество генерируемых аккаунтов на одного консьюмера - 5000/сутки и на всех консьюмеров - 25000/сутки, т.е. следует подходить взвешено к генерации тестовых аккаунтов, и стараться их переиспользовать между тестами по возможности.

### Hermione (E2e)

`npm run build` - Собрать

`npm run hermione:e2e -- <путь к тесту> --retry 0 -a` - Запустить тесты

Для возможности тестирования сценариев для авторизованных пользователей подключен плагин [`hermione-auth-commands`](https://github.yandex-team.ru/search-interfaces/infratest/tree/master/packages/hermione-auth-commands#команды).
Для авторизации достаточно воспользоваться командой `auth(login, options)`.
Однако обратите внимание на рекомендацию:
плагин разрабатывался в первую очередь для целей тестирования залогина на дампах, где высокая параллельность не требуется, и хотя технически плагин можно подключить и в e2e тесты, и при использовании только команды  auth с фиксированным набором используемых аккаунтов все должно будет работать, тем не менее, на данный момент жестких гарантий работоспособности плагина в условиях, отличных от снятия дампов, не дается.

### FAQ

#### Как исправить, когда тесты не проходят из-за того, что не находятся json-дамп в папке test-data?

Если запустить тест с опцией `--save` формируется папка `/<test-id>/<os-browser-device>/<url-id>.json.gz`. `test-id` - образуется из названия теста, `url-id` - образуется из того какой url открывается для снятия скриншотов. Поэтому когда убирается/добавляются флаги экспериментов, может потребоваться обновить дампы из-за изменения в `url-id`. 
Есть 2 варианта как исправить: перезапустить заново с опцией `--save` или переименовать `url-id` файла дампа json.gz. Переименование файла можно делать, если не изменились данные, связанные с новостью

#### Как образуется ссылки для .yaOpenUrl('news/story/a--789db9465a9dbba8dbd9cda8f6cde8a6')?
Ссылку на новость, которую видно в браузере можно сократить, тк только её окончание нужно для тестирования. Все что идет до `--` заменяют до 1 символа
