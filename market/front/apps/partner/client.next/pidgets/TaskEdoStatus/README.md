# TaskEdoStatus (Задача подключения к ЭДО)

<img src="https://media.github.yandex-team.ru/user/7930/files/c24d9a00-a931-11ec-97b2-4bb4d3692e0c" width="300">

## Общее описание

Виджет отображается в задачах сводки для партнеров, которые еще не подключились в электронному документообороту или
имеют задолженность по закрывающим документам. Ссылка в кнопке действия ведет на страницу закрывающих документов.

| Права               | Поля из AppState           | Модели | Фичи кокона |
| ------------------- | -------------------------- | ------ | ----------- |
| Доступен всем ролям | `campaignId`, `businessId` | Все    | -           |

## Используемые бэкенды

-   Проверка состояния приглашения партнера в системы операторов ЭДО (СБИС/ЮЗЭДО) - [getInvitationStatus](https://st.yandex-team.ru/MARKETBTOB-1551#609a8ecf5fb5070d0a8a3c22)
-   Получение информации о бизнесе партнера (информация о договорах) - [getContractsUsingGET](http://mbi-partner.tst.vs.market.yandex.net:38271/swagger-ui.html#/business-contracts-controller/getContractsUsingGET)
-   Получение списка проблем по договору (задолженность по закрывающим) - [getContractProblem](http://mbi-oebs-service.tst.vs.market.yandex.net/swagger-ui/index.html?url=/openapi/mbi-oebs-service.yaml#/contract%20problem/getContractProblem)
