# ZaloginPopup

<!-- description:start -->
Попап залогина
<!-- description:end -->

Использование:

```js
import { ZaloginPopup } from '@draft-components/components/ZaloginPopup/touch-phone/bundle';
```

## Базовый вариант
```js
const App = () => {
  const [visible, setVisible] = useState(false);
  const origin = 'serp__collections__geo_favorites_add';
  const passportHost = '//passport.yandex.ru';
  const service = 'serp';
  
  return (
    <div>
        <Button view="pseudo" size="m" onClick={() => setVisible((visible) => !visible)}>
            Показать попап
        </Button>
        <ZaloginPopup
            visible={visible}
            isSearchApp={false}
            title="Войдите в Яндекс"
            text="Тогда вы сможете оценивать отзывы и оставлять комментарии"
            hidePopup={() => setVisible(false)}
            passportParams={{ origin, passportHost, service }}
            isKubr={false}
        />
    </div>
    );
}
```

## Л-кука
Попап поддерживает л-куку для предложения пользователю авторизоваться последним аккаунтом, которым он
совершал вход. При авторизации сразу отправляет пользователя на страницу с полем ввода пароля.

## Аккаунт менеджер
Доступен в поисковом приложении, для авторизации используется нативное GUI приложения с хранилищем аккаунтов на устройстве. 

<!-- props:start -->
| Свойство       | Тип                    | Описание                                                                                              |
| -------------- | ---------------------- | ----------------------------------------------------------------------------------------------------- |
| title          | `string`               | Заголовок попапа                                                                                      |
| text           | `string`               | Текст попапа                                                                                          |
| passportParams | `IPassportParams`      | Параметры для формирования ссылка для авторизации через паспорт                                       |
| isKubr         | `false \| true`        | Признак домена (Казахстан, Украина, Беларусь, Россия). Нужен для правильного рендера дефолтной иконки |
| isSearchApp    | `false \| true`        | Признак поискового приложения, нужен для правильного отображения кнопок                               |
| nativeApi?     | `INativeApi`           | Нативное апи, для использования аккаунт менеджера, по умолчанию window.YandexApplicationsAPIBackend   |
| tension?       | `number`               | Параметры анимации шторки                                                                             |
| friction?      | `number`               | Описание отсутствует.                                                                                 |
| cookieL?       | `ICookieL`             | Л-кука пользователя, для саджеста аккаунта, которым он совершал вход ранее                            |
| designConfig?  | `IZaloginDesignConfig` | Дизайн конфигурация попапа                                                                            |
| hidePopup      | `() => void`           | Описание отсутствует.                                                                                 |
| visible        | `false \| true`        | Описание отсутствует.                                                                                 |
| onClose?       | `() => void`           | Описание отсутствует.                                                                                 |
<!-- props:end -->
