# Server

**app** собирается только бабелем и выполняется только в nodejs. Тут не должно быть обращений ко встроенным API браузера или специфичного клиентского кода.

## Server Side Rendering (SSR)

### renderOptions

#### Локализация

SSR не поддерживает работу с компонентом `I18n`, поэтому для вывода локализованного текста нужно использовать функцию `i18n`, которая передаётся в параметрах общей функции и в пропсах компонентов:
```jsx
import type {RenderOptions} from 'app/types/render';

// ...

const renderOptions: RenderOptions = {
    props: {
        // title принимает ID ключа и без вызова i18n
        title: 'pages.business-access-contact:title',
        // ...
    },
    components: {
        // Компоненты в пропсах получают i18n.
        BodyTitle: ({i18n}) => (
            <span>
                {i18n('pages.business-access-contact:page-header')}
            </span>
        ),
    }
};

// Получаем i18n в общей функции, если так удобнее.
const renderOptions: RenderOptions = ({i18n}) => ({
  // ...
});
```

Хардкодить русский текст крайне нежелательно потому, что это влечёт в будущем работу по выносу этого текста Танкер!

#### Селекторы для state

Иногда бизнес-логика требует провести вычисления над данными из state, при этом в `client.next` уже могут быть в наличии селекторы для чтения этих данных из state. В этом случае эти селекторы нужно вынести в `shared`.

Подключать селекоры из `client.next` нельзя!

#### Компоненты и сложная логика

Если в компоненте для `renderOptions`, например, для `Help`, есть сложная логика (чтение данных из state, условные операторы и т.д.), то имеет смысл вынети этот компонент в отдельный файл внутри папки `components` в папке страницы, например, в `app/stout/pages/html/PageAwesome/components/Help`.

#### Перевод страницы на SSR

При переводе страницы на SSR мы получаем, во-первых, более дружественную отрисовку страницы - на клиент уже прилетает что-то, а не пустой body, во-вторых, отказываемся от `yate`.

Перевести любую ПР страницу с `yate` на SSR очень [просто](https://i.pinimg.com/originals/72/29/5c/72295c2669305944b919e6320d436617.jpg):
- добавить `reactRenderOptions` в прототип страницы:
  ```typescript
  import type {RenderOptions} from 'app/types/render';
  // ...
  const renderOptions: RenderOptions = { /* ... */ };
  // ...
  HtmlPageName.prototype.reactRenderOptions = renderOptions;
  // ...
  ```
- удалить `yate`-шаблон страницы `client/desktop.pages/p-page-{{page-name}}`
- удалить поле `data.pageData.template` в конфиге роута для этой страницы
- в страничных АТ отключить ожидание BEM при открытии страницы, [пример](https://github.yandex-team.ru/market/partnernode/pull/5345/files#diff-34ee4d9958d09fae26fc7851d05a5506R64)
