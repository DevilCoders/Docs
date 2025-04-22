### Установка

Из папки `frontend` запустить команды:
```bash
npm ci && npm run bootstrap:hosts && npm run bootstrap:cert && npm run generate && npm run start
```


#### Форсинг версии в тестинге

```javascript
if (document.cookie.indexOf('static_version') === -1) { document.cookie = 'static_version=ХЭШ_КОММИТА_В_АРКАДИИ; path=/; expires=Tue, 19 Jan 2038 03:14:07 GMT'; console.log('Front cookie settled')} else { document.cookie = 'static_version=; Path=/; Expires=Thu, 01 Jan 1970 00:00:01 GMT'; console.log('Cookie deleted')}
```

#### Откат релиза

На странице с релизами выбрать нужную версию:
https://a.yandex-team.ru/projects/pricing-mgmt/ci/releases/timeline?dir=market%2Fpricing-management%2Fweb-app%2Ffrontend&id=frontent-release

И нажать на кнопку `Rollback to` у данной версии.
