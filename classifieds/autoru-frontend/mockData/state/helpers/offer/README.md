В этой директории лежат хелперы для того, чтобы создавать моки оферов с нужными параметрами.
Чтобы не клонировать каждый раз офер в каждом хелпере и для удобства вызова, нужно пользоваться функцией `cloneOfferWithHelpers`.
**ВАЖНО:** Чейнить можно только хелперы, в которых возвращается тот же объект, что и приходит __первым__ параметром.

Пример:

```javascript
    const offer = cloneOfferWithHelpers(groupCard)
        .withConfigurationNotice('GT')
        .withConfigurationTags([ 'new4new' ])
        .withIsOwner()
        .value();
```
