# Написание безопасных удаленных резолверов

`createSafeResolver` - это надстройка над createResolver из mandrel для проверки прав доступа к запросу

## Использование
Параметры у createSafeResolver те же, что у createResolver, но в settings добавляется объект cocon

### Если `settings.remote` не указан
createSafeResolver работает так же, как createResolver из mandrel

### Если `settings.name` находится в [noCheckRemoteResolversNames](noCheckRemoteResolversNames.ts)
В этом случае createSafeResolver тоже работает как createResolver из mandrel

**WARNING**: в этом случае запрос из резолвера сможет делать любой залогиненный в партнерку пользователь!!!

Новые резолверы **не следует добавлять в noCheckRemoteResolversNames** (кроме случаев, когда ничего страшного от вызова резолвера сторонним пользователем не будет), они нужны только для безболезненного перехода на новый createResolver

### В остальных случаях
В settings надо передать объект cocon для проверки прав доступа

#### TLDR
```javascript
const resolveData = createResolver(impl, {
    name: 'resolveData',
    remote: true,
    cocon: {
        campaignIdMapper: ({someCampaignIdParam}) => someCampaignIdParam,
        group: RESOLVER_GROUP.ALL_WITH_CABINET_ACCESS
    },
    // остальные параметры createResolver, например,  cache или errorHandler   
})
```
Такая конфигурация убережет резолвер от вызова пользователем без доступа к соответствующему кабинету<br><br>

#### Подробное объяснение:

Допустим, мы хотим создать резолвер `resolveData`

##### Правим кокон

Определяемся, какую группу доступа из [resolverGroups](https://github.yandex-team.ru/market/market-tpl-front/blob/master/shared/constants/resolverGroups.ts) будет использовать резолвер

##### Как выбрать группу доступа?
>Стоит выбирать ту, что ближе по смыслу к использованию резолвера (в комментах resolverGroups описано, за что каждая группа отвечает) 
<br>Если все равно непонятно, какую использовать, можно воспользоваться `ALL_WITH_CABINET_ACCESS`

Допустим, мы выбрали группу `GROUP_NAME` (для примера, в константе resolverGroups такой группы нет)

Сначала возможно потребуется сделать правки в конфиге кабинета в коконе
https://a.yandex-team.ru/arc/trunk/arcadia/market/mbi/cocon/cabinet-configs/src/main/resources/cabinets/

##### Как понять, какой кабинет нам нужен?
>
>Если `resolveData` вызывается на странице с урлом вида
>
>```/some/route/somePlatform/foo/bar```
>
>и конфиг этой страницы имеет вид
> ```javascript
> {
>    // ...
>    pattern: '/some/route/<platformType>/foo/bar'
> }
>```
>
>То нам  нужен конфиг кабинета `somePlatform.json`

Для работы резолвера в конфиге должна содержаться фича `GROUP_NAME` на странице `resolvers-groups`
```json5
{
  // ...
  "pages": [
    {
      "name": "resolvers-groups", 
      // в features содержится список групп прав доступа
      "features": [
        // ...,
        {
          // название нужной группы
          "name": "GROUP_NAME"
          // далее указываем разные проверки кокона для этой группы
          // если проверки не нужны - стоит воспользоваться уже прописанной "ALL_WITH_CABINET_ACCESS"
        }
        // ...
      ]
    }
  ]
}
```

##### Создаем резолвер с параметрами доступа к кокону

Создание безопасного резолвера похоже на создание обычного с той разницей, что в настройки `createResolver`
добавляется объект `cocon` с параметрами доступа к кокону:

**Параметры объекта `cocon`:**

###### group
>Единственное обязательное поле, содержит ранее выбранную нами группу доступа

Далее следуют два похожих необязательных поля для мапинга параметров 

###### businessIdMapper
>Если для доступа к выбранной группе в коконе нужен `bussinessId`, надо передать функцию,
>которая из параметров резолвера будет получать `bussinessId` (либо название параметра, в котором `bussinessId` содержится)

###### <br>campaignIdMapper
>Если для доступа к выбранной группе в коконе нужен `campaignId`, надо передать функцию,
>которая из параметров резолвера будет получать `campaignId` (либо название параметра, в котором `campaignId` содержится)

###### <br>cabinetTypeMapper 
>
>В большинстве случаев не нужен
>
>Но если в [паттерне страницы, с которой вызывается резолвер](https://github.yandex-team.ru/market/market-tpl-front/blob/master/shared/utils/createSafeResolver/README.md#как-понять-какой-кабинет-нам-нужен) нет параметра `<platformType>`,
>`createSafeResolver` не сможет самостоятельно определить, к какому кабинету в коконе обращаться
>
>В этом случае нужно будет указать функцию-маппер для получения названия кабинета из контекста и параметров резолвера
>```javascript
>campaignIdMapper: (ctx, paramms) => params.platformParam
>```

<br>Допустим, в нашем случае 
* `campaignId` нужен для доступа к кокону и заключен в параметре `somePlatformId`
* `businessId` не нужен для доступа к кокону
* `<platformType>`, в конфиге страницы указан 

Значит, наш резолвер будет создаваться вот так: 

```javascript
const resolveData = createResolver(impl, {
    name: 'resolveData',
    remote: true,
    // параметры для доступа к кокону
    cocon: {
        campaignIdMapper: ({somePlatformId}) => somePlatformId,
        group: RESOLVER_GROUP.GROUP_NAME,
    },
    // еще какие-то настройки резолвера по вкусу, например cache или errorHandler
  });
```

Теперь перед вызовом имплементации `resolveData` ПИ будет ходить в кокон и проверять, есть ли у пользователя
права к фиче `GROUP_NAME` на странице `resolvers-groups` в кабинете `somePlatform`
