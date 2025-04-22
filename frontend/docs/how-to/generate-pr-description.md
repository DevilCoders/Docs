# Генерация описания пулл-реквеста

Автоматически обновляет описание пулл-реквеста, проставляет ссылки на беты сервисов.
Обновление выполняется в задаче `Update PR Description` [trendbox-ci](https://github.yandex-team.ru/search-interfaces/trendbox-ci) и занимает около 3-4 минут.

Треубется создать конфиг `services/{ID_сервиса}/.config/pr-description-config.js` со следующим содержимым:
```javascript
module.exports = {
    service: '{ID_сервиса}',
    '@title': '{название_сервиса}',
    '@iconUrl': 'https://github.yandex-team.ru/images/icons/emoji/unicode/1f4f1.png',
    pipeLinks: [
        {
            label: 'Бета',
            url: '{URL_беты}',
            qr: true,
        },
    ],
};
```

Подробнее про настройку см. [документацию](https://github.yandex-team.ru/search-interfaces/microservices/blob/master/services/prosperity/docs/pr-description-v2.md#pipelinks)
