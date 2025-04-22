# Личный кабинет

Содержание:

-   [Точки входа](#entry-points)
-   [Параметры форм](#params):
    -   [Общие параметры всех форм](#common-params)
    -   [Вкладка "Впечатления"](#impressions)
    -   [Вкладка "Задания"](#assignments)
    -   [Вкладка "Зеркала"](#mrc)
    -   [Вкладка "Отзывы"](#reviews)
    -   [Вкладка "Фото"](#photos)
    -   [Вкладка "Исправления"](#feedback)
-   [Проброс авторизации из мобильного клиента](#mobile-auth)
-   [Параметры для пуш нотификаций](#pushes)
-   [Возвращение в мобильный клиент](#mobile-back)

<div id=entry-points></div>

## Точки входа

| env        | url                                                                     |
| ---------- | ----------------------------------------------------------------------- |
| testing    | https://l7test.yandex.ru/maps/<br/>https://l7test.yandex.com/maps/<br/> |
| production | https://yandex.ru/maps/<br/>https://yandex.com/maps/                    |

<div id=params></div>

## Параметры форм

<div id=common-params></div>

### Общие параметры всех форм

| query arg             | type                                                                                                                                                                                                                    | required | description                                                                                                                                                                                                                                                                                                |
| --------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| client_id             | ru.yandex.yandexmaps<br/>ru.yandex.traffic<br/>ru.yandex.traffic.sandbox<br/>ru.yandex.yandexmaps.debug<br/>com.yandex.maps.TestApp<br/>com.yandex.maps.testapp</br>ru.yandex.yandexnavi<br/>ru.yandex.mobile.navigator | ✔        | [ID клиента](https://wiki.yandex-team.ru/maps/feedback/newfeedback/clientid/).                                                                                                                                                                                                                             |
| context               | string                                                                                                                                                                                                                  |          | [Идентификатор](https://wiki.yandex-team.ru/maps/feedback/newfeedback/clientcontextid/) точки входа в формы фидбека на стороне клиента.                                                                                                                                                                    |
| uuid                  | string                                                                                                                                                                                                                  |          | uuid пользователя из AppMetrika. Только для мобильных клиентов.                                                                                                                                                                                                                                            |
| deviceid              | string                                                                                                                                                                                                                  |          | deviceid пользователя из AppMetrika. Только для мобильных клиентов.                                                                                                                                                                                                                                        |
| lang                  | string                                                                                                                                                                                                                  |          | Язык или локаль пользователя. От этого параметра зависит язык интерфейса форм и отображение подложки на карте. Если параметр передан не будет, то будет использовано автоматическое определение локали с помощью [langdetect](https://doc.yandex-team.ru/lib/lang-detect/concepts/lang-detect-descr.html). |
| webview               | true                                                                                                                                                                                                                    |          | Для мобильных клиентов.                                                                                                                                                                                                                                                                                    |
| theme                 | dark                                                                                                                                                                                                                    |          | Тема интерфейса. Используется только в WebView.                                                                                                                                                                                                                                                            |
| safearea_inset_top    | number                                                                                                                                                                                                                  |          | Отступ контента сверху для отображения в SafeArea в WebView.                                                                                                                                                                                                                                               |
| safearea_inset_bottom | number                                                                                                                                                                                                                  |          | Отступ контента снизу для отображения в SafeArea в WebView.                                                                                                                                                                                                                                                |
| application_version   | string                                                                                                                                                                                                                  |          | Версия мобильного приложения.                                                                                                                                                                                                                                                                              |

<div id=impressions></div>

### Вкладка "Впечатления"

Для использования необходимо использовать `URL PATH: /profile/ugc/impressions`.
Дополнительные параметры отсутствуют.

**Пример: https://yandex.ru/maps/profile/ugc/impressions/?client_id=ru.yandex.yandexmaps&uuid=38c285c4-777e-a5d6-7caf-a169df3bce6a&deviceid=12345&webview=true**

<div id=assignments></div>

### Вкладка "Задания"

Для использования необходимо использовать `URL PATH: /profile/ugc/assignments`.
Дополнительные параметры отсутствуют.

**Пример: https://yandex.ru/maps/profile/ugc/assignments/?client_id=ru.yandex.yandexmaps&uuid=38c285c4-777e-a5d6-7caf-a169df3bce6a&deviceid=12345&webview=true**

#### Логирование

##### Логирование ЛК для дашбордов

Описание контракта логирования можно найти в [документации фидбека](./feedback.md#analytics)
Дополнительные поля в метадате событий для заданий ЛК:

| field name      | type   | description                                                                                                            |
| --------------- | ------ | ---------------------------------------------------------------------------------------------------------------------- |
| assignment_id   | string | Идентификатор задания.                                                                                                 |
| assignment_type | string | [Тип задания](../src/ugc-profile/assignments/types/assignments.ts#L105). |

###### Пример использования в ЛК

Логирование формы редактирования задания в ЛК:

```jsx
<UgcContractAnalyticsWrapper
    isForm
    name="assignment_form"
    config={props.config}
    assignment={assignment}
    context={{formContextId: '...'}}
>
    <AssignmentEditView />
</UgcContractAnalyticsWrapper>
```

Логирование кнопки отправки фидбека в форме редактирования задания ЛК:

```jsx
<UgcContractAnalyticsWrapper
    isSubmitButton
    name="submit"
    config={props.config}
    assignment={assignment}
    context={formContextId: '...'}
    logClick
>
    <FeedbackLoadableButton text={i18n('feedback', 'submit')} onClick={this.onSubmit()} />
</UgcContractAnalyticsWrapper>
```

##### Логирование активных элементов в ЛК

В метадате событий используются следующие поля:

| field name      | type   | description                                                                                                                                                |
| --------------- | ------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------- |
| assignment_id   | string | Идентификатор задания.                                                                                                                                     |
| assignment_type | string | [Тип задания](../src/ugc-profile/assignments/types/assignments.ts#L105).                                     |
| formType        | string | Тип формы для заданий ЛК. [Посмотреть весь список](../src/feedback/common/types/feedback-common.ts#L30-L37). |

###### Пример использования в ЛК

Логирование карточки задания в ленте:

```jsx
<UgcAnalyticsWrapper name="card" logViewportEnter="when appears on screen" assignment={assignment}>
    <UgcAdressAssignmentCard assignment={assignment} />
</UgcAnalyticsWrapper>
```

Логирование кнопки "Пропустить":

```jsx
<UgcAnalyticsWrapper name="skip" assignment={assignment} logClick>
    <Button onClick={this._onSkipClick}>{i18n('user-profile', 'assignments-skip')}</Button>
</UgcAnalyticsWrapper>
```

<div id=mrc></div>

### Вкладка "Зеркала"

Для использования необходимо использовать `URL PATH: /profile/ugc/mrc`.

#### Дополнительные параметры

| query arg | type   | required | description                               |
| --------- | ------ | -------- | ----------------------------------------- |
| oid       | string |          | Идентификатор маршрута для редактирования |

**Пример: https://yandex.ru/maps/profile/ugc/mrc/?webview=true&oid=2020&client_id=ru.yandex.yandexmaps**

<div id=reviews></div>

### Вкладка "Отзывы"

Для использования необходимо использовать `URL PATH: /profile/ugc/reviews`.

#### Дополнительные параметры

| query arg | type   | required | description               |
| --------- | ------ | -------- | ------------------------- |
| oid       | string |          | Идентификатор организации |

**Пример: https://yandex.ru/maps/profile/ugc/reviews?webview=true&oid=137418485493&client_id=ru.yandex.yandexmaps**

<div id=photos></div>

### Вкладка "Фото"

Для использования необходимо использовать `URL PATH: /profile/ugc/photos`.

| query arg  | type                     | required | description                                              |
| ---------- | ------------------------ | -------- | -------------------------------------------------------- |
| photos_tab | account<br/>organization |          | Открытая вкладка во вкладке Фото. По умолчанию `account` |

**Пример: https://yandex.ru/maps/profile/ugc/photos?webview=true&client_id=ru.yandex.yandexmaps**

<div id=feedback></div>

### Вкладка "Исправления"

Для использования необходимо использовать `URL PATH: /profile/ugc/feedback`.
Дополнительные параметры отсутствуют.

**Пример: https://yandex.ru/maps/profile/ugc/feedback?webview=true&client_id=ru.yandex.yandexmaps**

<div id=mobile-auth></div>

## Проброс авторизации из мобильного клиента

Для проброса авторизации из мобильного клиента необходимо устанавливать куки через метод `requestCookieAuthURLWithAccount` в AccountManager.
Подробнее можно прочитать в [документации](https://wiki.yandex-team.ru/yandexmobile/accountmanager/help/ios/lastapi/#yalcookieexchangerobmenxtokenanaavtorizacionnyekuki).

<div id=pushes></div>

## Параметры для пуш нотификаций

### Приоритизация карточки задания

Для поднятия приоритета карточки задания в карусели ленты необходимо в URL указать сслледующие параметры:

| query arg     | type   | required | description           |
| ------------- | ------ | -------- | --------------------- |
| assignment_id | string |          | Идентификатор задания |

**Пример: https://yandex.ru/maps/profile/ugc/assignments/?client_id=ru.yandex.yandexmaps&uuid=38c285c4-777e-a5d6-7caf-a169df3bce6a&deviceid=12345&webview=true&assignment_id=os:175467174304**

### Приоритизация карточки пользовательского вклада

Для поднятия приоритета карточки задания в карусели ленты необходимо в URL указать сслледующие параметры:

| query arg       | type   | required | description          |
| --------------- | ------ | -------- | -------------------- |
| contribution_id | string |          | Идентификатор вклада |

**Примеры:**

-   **Вкладка "Исправления": https://yandex.ru/maps/profile/ugc/feedback/?client_id=ru.yandex.yandexmaps&uuid=38c285c4-777e-a5d6-7caf-a169df3bce6a&deviceid=12345&webview=true&contribution_id=fb:175467174304**
-   **Вкладка "Фото": https://yandex.ru/maps/profile/ugc/photos/?client_id=ru.yandex.yandexmaps&uuid=38c285c4-777e-a5d6-7caf-a169df3bce6a&deviceid=12345&webview=true&photos_tab=account&contribution_id=pht:175467174304**
-   **Вкладка "Зеркала": https://yandex.ru/maps/profile/ugc/mrc/?client_id=ru.yandex.yandexmaps&uuid=38c285c4-777e-a5d6-7caf-a169df3bce6a&deviceid=12345&webview=true&contribution_id=mrc_ride:175467174304**

## Возвращение в мобильный клиент

При использовании через WebView после завершения рабты в WebView необходимо его закрыть.
Для этого мобильный клиент должен подключить JS Api и дать возможность закрывать WebView используя метод yandex.mapsApp.close из объекта Window.
