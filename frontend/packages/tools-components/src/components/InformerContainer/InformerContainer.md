# InformerContainer

<a
  href='https://github.yandex-team.ru/search-interfaces/frontend/tree/master/packages/tools-components/src/components/InformerContainer'
  target='_blank'>
  <img
    src='https://badger.yandex-team.ru/custom/[Исходники]/[Github][green]/badge.svg'
  />
</a>

Компонент, предназначенный для отображения информационных уведомлений.
Представляет из себя `MessageBox`, который выводится в правом нижнем углу окна браузера, следуя заданным в конфигурации правилам отображения.
Используется в паре с [`express-informer-middleware`](https://github.yandex-team.ru/search-interfaces/frontend/tree/master/packages/express-informer-middleware).

Настройка уведомлений происходит в [Бункере](https://bunker.yandex-team.ru/informer/informers).
Для своего проекта необходимо создать узел внутри кластера `informer/informers`, и позже передать его путь (относительно `informer/informers`) в `props` в поле `node`.
по заданной `JSON`-схеме.

Пример `JSON` узла:

```js
{
  // Техническое поле, его обновление сбрасывает локальный "кеш" в LocalStorage пользователя
  "keyEpoch": "0",
  // Время перед показом информера после загрузки страницы (секунды)
  "beforeShowTimeout": 5,
  // Время между показами разных информеров (минуты)
  "informerInterval": 5,
  "informers": [
    {
      // Минимальное время между показами этого информера (минуты)
      "currentInformerTimeout": 1,
      // ID информера (ОБЯЗАН БЫТЬ УНИКАЛЬНЫМ)
      "id": "coronavirus",
      // Заголовок информера (можно задавать в N языках)
      "title": {
        "ru": "Вторая волна",
        "en": "The second wave"
      },
      // Ссылка на иконку информера (отображается в левом верхнем углу информера)
      "iconUrl": "https://jing.yandex-team.ru/files/tet4enko/pngwing.com.png",
      // Текст информера (можно задавать в N языках)
      "text": {
        "ru": "Давайте посидим дома",
        "en": "Let's stay at home"
      },
      "button": {
        // Текст кнопки (можно задавать в N языках)
        "text": {
          "ru": "Посмотреть статистику (latest)",
          "en": "See stats"
        },
        // Ссылка, по которой будет осуществлен переход при нажатии на кнопку (необязательное поле)
        // при отсутсвии данного поля, при нажатии на кнопку информер будет закрываться
        "link": "https://coronavirus-monitor.ru/"
      }
    }
  ]
}
```

## Принцип работы

Через `beforeShowTimeout` секунд показыватся случайный информер из списка тех, что
 * еще не были закрыты 
 * прошло `currentInformerTimeout` минут после последнего отображения данного информера
 * прошло `informerInterval` минут после последнего отображения любого последнего информера
Данные о таймингах и факте закрытия информеров берется из `LocalStorage` клиента.

Если информер был закрыт, через минимально возможное время будет показан информер, который может быть показан быстрее всех (исходя из таймингов).


## Пример подключения

```jsx
import { InformerContainer } from '@yandex-int/tools-components/InformerContainer/desktop';

// ***

<InformerContainer
    route='/informer-route'
    node='/wiki/intranet'
    lang='ru'
>
```

## Свойства

| Свойство    | Тип                                                                                                                                                                                                                                                               | По умолчанию | Описание                                                                                                                               |
| ----------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ | -------------------------------------------------------------------------------------------------------------------------------------- |
| className?  | `string`                                                                                                                                                                                                                                                          | —            | Дополнительный className                                                                                                               |
| route       | `string`                                                                                                                                                                                                                                                          | —            | `pathname`, на который будет делаться запрос за конфигурацией, и на который должна быть настроена миддлварь [`express-informer-middleware`](https://github.yandex-team.ru/search-interfaces/frontend/tree/master/packages/express-informer-middleware) |
| node        | `string`                                                                                                                                                                                                                                                          | —            | путь к узлу конфигурации в Бункере, относительно `informer/informers`                                                                  |
| lang        | `string`                                                                                                                                                                                                                                                          | 'ru'         | Язык, на котором будет отображен информер                                                                                              |
| lockedInformers        | `string[]`                                                                                                                                                                                                                                                          | []           | ID информеров, которые нельзя показывать в данный момент                                                                                              |
