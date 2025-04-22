# Обработка ошибок

На текущий момент есть два основных класса ошибок, наследующихся от `Error`:
- *Клиентские* (ClientError): `static/common/isomorphic/errors/ClientError`
- *Серверные* (ServerError): `static/common/isomorphic/errors/ServerError`

*Клиентские* ошибки можно генерировать самостоятельно при необходимости добавить дополнительную информацию об ошибке, например, в случае когда нужно поднять ошибку валидации с определенным сообщением.

*Серверные* ошибки возникают в случае неудачных запросов к API. *Серверная* ошибка хранит код ответа в `ServerError.status` и тело ответа в `ServerError.body`. Тело ответа может содержать информацию, на основании которой можно сгенерировать сообщение для пользователя о возникшей ошибке. На основе информации из *серверной* ошибки может быть сгенерирован `antd.notification`, информация может каким-то образом отображаться на текущей странице/окне. Тело ответа может содержать одну пользовательскую ошибку или список таких ошибок, например:
```JavasSript
{errors: [
    {
      "code": "missing_mandatory_parameter",
      "details": {
        "field": "efficiency_time",
        "entity_type": "group",
        "entity_name": "Имя группы",
        "entity_id": "7606"
      }
    }
]}
```
Приведенная выше ошибка говорит об отсутствии обязательного параметра `efficiency_time` у одной из групп в кампании, в данном случае у группы с идентификатором `7606`(идентификатор группы уникален в рамках конкретной кампании).
Список ошибок может также, помимо прочих ошибок, содержать аналогичную ошибку, но на параметр `efficiency_date`. В данном кейсе, в соответствии с [TEF-1847](https://st.yandex-team.ru/TEF-1847), мы выводим сообщение вида:
`Не указаны время и период коммуникации в группах: ${entityNames.joinn(', ')}`.

Для отображения в том числе подобного рода сообщений на основе одной или группы ошибок существует утилита `getNotificationErrorHandler` (`static/common/utils/errors/errorHandlers`).

## Функция getNotificationErrorHandler

`getNotificationErrorHandler` - функция высшего порядка, создающая *обработчик ошибок*. *Обработчик* ошибок может быть использован, например, в `catch`-е ассинхронной функции или в колбэке `onError` мутации. Обработчик не обязательно должен обрабатывать ошибку, при помощи него можно вывести определенное сообщение по факту возникновения какой-либо ошибки.

> NOTE: Все запросы к API должны содержать хотя-бы один обработчик

```JavaScript
getNotificationErrorHandler(message, {
    handlers,
    propagate,
    notificationProps
})
```
- *message* - Основное сообщение об ошибке. Отобразится в заголовке нотификации
- *options*:
  - *handlers* - массив *обработчиков ошибок*, через которые будет пропущен массив ошибок.
  - *propagate* - флаг, пробрасывать ли ошибку в исходном виде далее после успешной обработки (default: `false`)
  - *notificationProps* - дополнительные [настройки конфига](https://ant.design/components/notification/#API) `antd.notification`(`message` и `decription` будут сгенерированы по результатам обработки ошибки с помощью `handlers`)

По результату выполнения обработчик ошибок выведет `notification.error({message, description, ...notificationProps})`, где `description` - полученный в результате прохода всех обработчиков массив сообщений, разделенный при помощи [Divider](https://ant.design/components/divider/).

Пример использования `getNotificationErrorHandler` при запросе к API:

```JavaScript
// запрашиваем параметры сегмента
CampaignApi.requestCampaign(campaign.id)
    .catch(
        getNotificationErrorHandler(
            'Не удалось загрузить кампанию',
            {
                handlers: CAMPAIGN_REQUEST_ERROR_HANDLERS, // обработчики ошибок, которые могут возникать при данном запросе
                notificationProps: {
                    duration: 5 // показываем сообщение в течении 5 секунд
                }
            }
        )
    );
```

### Обработчики ошибок

*Обработчик ошибок* - функция с сигнатурой `(data: ErrorHandleFlowData) => ErrorHandleFlowData`, где:

```typescript
type ErrorHandleFlowData = {
    restErrors: Error[];
    messages: ReactNode[];
}
```
Обработчики ошибок хронятся в папке `queries/error-handlers` соответсвующего бандла.

Предполагается что каждый обработчик примет на вход список необработанных ошибок, найдет среди них те, с которыми он умеет работать, добавит сообщение в массив `messages` на основе информации из найденных ошибок, и вернет список ошибок без обработанных им ошибок и список сообщений, включающий сгенерированное в ходе обработки. Возвращаемые обработчиком данные будут переданы на вход следующему обработчику.

Массив `restErrors` может содержать ошибке разного типа. Для *серверных ошибок*, содержащих в теле массив `errors`, на вход первому обработчику в `restErrors` поступит массив инстансов `ServerError`, каждый из которых в `body` будет содержать соответствующую ошибку из массива `errors` в исходном виде.

Обработчики, предназначенные для обработки серверных ошибок, могут использовать отделюную функцию, которая попытается извлечь ошибку в исходном виде из тела `Error`. Пример такой функции:
```typescript
export const extractValidationError = (error: Error): ValidationError | false => {
    return (
        (
            error instanceof ServerError &&
            'code' in error.body &&
            'details' in error.body &&
            (
                'field' in error.body.details ||
                'reason' in error.body.details
            )
        ) &&
        error.body as unknown as ValidationError
    );
};
```
Данная функция определяет объект типа `ValidationError` в теле `ServerError` по наличию в нем поле: `code`, `details.field`, `details.reason`.

В случае успешного извлечения ошибки определенного типа, обработчик проводит проверку кода ошибки и прочих полей(например, `reason`), необходимую ему для того чтобы определить, может ли он вывести зашитое в нем сообщение на основании данной ошибки. Пример обработчика:
```JavaScript
export const efficiencyStopTimeExpiredErrorHandler: ErrorHandler = ({messages, restErrors}) => {
    const errors = restErrors.filter(error => {
        const campaignSendError = extractValidationError(error);

        if (
            !campaignSendError ||
            campaignSendError.code !== ValidationErrorCode.CampaignEfficiencyStopTimeExpired
        ) {
            return true;
        }

        messages.push(
            <div key="efficiency-stop-time-expired">
                Дата завершения Актуальности кампании должна быть в будущем.
            </div>
        );
    });

    return {messages, restErrors: errors};
};
```

> NOTE: Элемент, добавляемый в массив `messages`, должен содержать ключ, уникальный в рамках массива

## Прочие кейсы

В случае, если ошибка требует каких-либо действий в рамках компонента, например, подсветку полей формы, это можно также сделать из `catch` запроса. Если помимо этого запрос содержит обработчик, созданный с помощью `getNotificationErrorHandler`, в конфиг `getNotificationErrorHandler` нужно передать флаг `propagate` или повесить обработчик после `catch`-а, содержащего логику подсветки формы. Пример:

```typescript
someMutation.mutateAsync()
    .then(() => {
        notification.success({message: 'Успешно добавили что-то'});
    })
    .catch(
        getNotificationErrorHandler(
            'Не удалось отправить что-то',
            {
                handlers: SEND_SOME_ERROR_HANDLERS,
                propagate: true
            }
        )
    )
    .catch((e: Error) => {
      // сделать что-то на основе e
    });
```
