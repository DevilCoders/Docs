# csp-logger

Данный пакет позволяет подписываться на событие нарушения CSP ([SecurityPolicyViolationEvent](https://developer.mozilla.org/en-US/docs/Web/API/SecurityPolicyViolationEvent)) и отправлять репорты в https://csp.yandex-team.ru.

По сути это замена `report-to` для подсервисов, у которых нет возможности контролировать заголовок `Content-Security-Policy` страницы.

## Подключение

Для отправки репортов необходимо создать экземпляр класса `CSPLogger`. Конструктор класса `CSPLogger` первым аргументом  принимает тип `CSPLoggerConfig`, в котором указываются основные (неизменяемые) параметры логов. Вторым аргументом - объект с дополнительными параметрами, которые необходимы проекту.

Пример:
```
const csp = new CSPLogger(
    {
        from: config.streamPlayerParams.source.params.additionalParams.from,
        slots: config.streamPlayerParams.source.params.additionalParams.slots,
        project: 'video-player',
        version: VERSION,
        yandexuid: getCookie(document, 'yandexuid'),
        yandex_login: getCookie(document, 'yandex_login'),
    }, {
        vsid: config.streamPlayerParams.source.params.additionalParams.vsid,
    }
);
```

## API 

* `subscribe(doc: Document): void` - метод для подписки на событие `SecurityPolicyViolationEvent` из документа `doc`
Пример:
```
csp.subscribe(iframe.contentDocument);
```

* `unsubscribe(doc: Document): void` - метод для отписки от события `SecurityPolicyViolationEvent` из документа `doc`
Пример:
```
csp.subscribe(iframe.contentDocument);
```

* `setAdditional` - метод для изменения дополнительных параметров, отправляемых вместе с логами
```
csp.setAdditional({
    content_id: config.streamPlayerParams.source.params.additionalParams.content_id 
    // теперь в дополнительных параметрах будет отправляться не только vsid, но и content_id
});
```
