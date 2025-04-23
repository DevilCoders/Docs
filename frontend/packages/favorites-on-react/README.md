# favorites-on-react
Библиотека для подключения [Я.Избранного](https://yandex.ru/collections) на сервисы

## Возможности
- оборачивает под собой запросы в API Избранного
    - получение CSRF-токена
    - запросы в ручки добавления/удаления/получения статуса карточек ([ручки](https://wiki.yandex-team.ru/collections/ruchki-dlja-edinogo-izbrannogo/#ruchkaproverkidobavlennostiurla))
- открывает IFrame для выбора коллекции, в которую нужно добавить документ (ссылку)
- предоставляет [компонент](./src/desktop/Favorites.tsx), который принимает компоненты для показа статуса наличия ссылки/документы в Избранном
- реализует [гайдлайны Избранного](https://wiki.yandex-team.ru/users/kulikov-sasha/favorites-guidelines/) - попапы/привязки к элементам/добавления/удаления
- иконки/кнопки определяет СЕРВИС, который встраивает библиотеку

## Подключение на сервис
<ul>
<li><a href="https://a.yandex-team.ru/arc/trunk/arcadia/frontend/projects/lego/packages/rpc">@yandex-lego/rpc</a> нужна для общения с IFrame</li>
<li>в вашем сервисе используется React >= 16.8.x</li>
<li>

добавлены CSP-правила для открытия IFrame добавления в коллекцию. Нужно добавить возможность открывать в IFrame с урлов с `yandex.${csp.TLD}`, `*.yandex.${csp.TLD}`;</li>
<li>написана прокси для похода с локального сервиса (http://localhost:8080/collections) на https://l7test.yandex.ru/collections

<details>
<summary>Пример middleware для котика:</summary>

```javascript
// файл конфига котика
{
    matcher: req => req.kotik.parsedURL.pathname.startsWith('/collections'),
    handler: [{ name: 'collectionsController', fn: collectionsController }],
},

// файл middleware
const { createProxyMiddleware } = require('http-proxy-middleware');

let proxy;

function collectionsController(req, res, next) {
    if (!proxy) {
        proxy = createProxyMiddleware({
            target: 'https://l7test.yandex.ru',
            changeOrigin: true,
            secure: false,
        });
    }

    return proxy(req, res, next);
}

module.exports = {
    collectionsController,
};
```

</details>
</li>
<li>

в конфиг webpack добавлен alias на @yandex-lego (это нужно, чтобы при сборке для бет, тестинга и прода в сервисе и в библиотеке использовалась одна копия @yandex-lego). Пример:

```
alias: {
    '@yandex-lego': path.resolve('node_modules/@yandex-lego'),
},
```
</li>
</ul>

## Как использовать
Пример внедения можно посмотреть [тут](https://a.yandex-team.ru/review/1950471/files/813a7c07fd851645837711df51871ca7916539f1)
- `npm i @yandex-int/favorites-on-react @yandex-lego/rpc`
- разные сборки для desktop/touch
    - `export { Favorites } from '@yandex-int/favorites-on-react/build/components/desktop';`
    - `export { Favorites } from '@yandex-int/favorites-on-react/build/components/touch-phone';`
- тайпинги и утилиты здесь
    - `import { IFavoritesProps } from '@yandex-int/favorites-on-react';`

### Компонент Favorites
- необходимо импортировать компонент Favorites для нужной платформы (см. выше)
- Favorites принимает следующие параметры:
```typescript
export interface IFavoritesProps {
    // Вам точно пригодяться эти
    /** Карточка из Я.Избранное */
    card: ICard;
    /** Залогинен ли пользователь */
    loggedIn: boolean;
    /** URL по которому может залогинется пользователь */
    loginUrl: string;
    /** Компонент удаления из избранного */
    buttonRemove: React.FC<IFavoritesButtonRemoveProps>;
    /** Компонент добавления в избранное */
    buttonAdd: React.FC<IFavoritesButtonAddProps>;
    /** id аватара пользователя */
    avatarId?: string;
    /** Кол-во мс которые показывается попап после успешного действия */
    popupTimeout?: number;
    /** Обработчик сохранения карточки в избранное */
    onFavoritesSaved?: (card: ICard | undefined) => void;
    /** Обработчик удаления карточки из избранного */
    onFavoritesRemoved?: () => void;
}
```
- card можно создать с помощью функции `import { getFavoritesCard } from '@yandex-int/favorites-on-react';`
- все свойства доступны [здесь](./src/Favorites/Favorites.typings/index.ts)

### FavoritesController
Контроллер, который умеет добавлять/удалять/проверять статусы карточек в Избранном.
Добавлять/удалять карточки в ручную не нужно, а вот проверить статус может пригодиться, если с бека вам не приходит информация об избранном. Примеры:
```javascript
import { ILinkStatusAnswer, FavoritesController } from '@yandex-int/favorites-on-react';

FavoritesController.getInstance().isUrlInFavorites(url, loggedIn)
FavoritesController.getInstance().isUrlsInFavorites(urls, loggedIn)
```

## Как разрабатывать библиотеку
Пример по интеграции с сервисом [Товарную вертикаль (ТВ)](https://a.yandex-team.ru/arc/trunk/arcadia/frontend/services/goods)
- зайти в директорию библиотеки https://a.yandex-team.ru/arc/trunk/arcadia/frontend/packages/favorites-on-react
- собрать ее командой `npm link`
- перейти в [ТВ](https://a.yandex-team.ru/arc/trunk/arcadia/frontend/services/goods)
- установить зависимости, следуя их гайду
- добавить дополнительный alias в конфиг вебпака для react (это нужно, чтобы при одновременной разработке библиотеки и сервиса не тянулась версия реакта из библиотеки и не было <a href="https://reactjs.org/docs/error-decoder.html/?invariant=321">падений</a>)
  ```
  alias: {
      react: path.resolve('node_modules/react/'),
  },
  ```
- слинковать библиотеку `npm link @yandex-int/favorites-on-react`
- запустить ТВ

## Планы
- причесать API (убрать loginURL, передавать url, а не карточку, более плавные анимации)
- переводы - https://st.yandex-team.ru/PODB-21287
- пожелания заводить подзадачей https://st.yandex-team.ru/PODB-20441
- библиотека сделана на основе кода из [Fiji](https://aa.yandex-team.ru/arc/trunk/arcadia/frontend/projects/fiji/sakhalin/src/components/Favorites), некоторые части будут убраны/переработаны
