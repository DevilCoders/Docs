# StarTrek API Client [![Build Status](https://drone.yandex-team.ru/api/badges/toolbox/st-client/status.svg?branch=master&style=flat)](https://drone.yandex-team.ru/toolbox/st-client)

Клент для API стартрека. Легкий, простой, прозрачный. Постороен на основе Promise.

[Описание API](https://wiki.yandex-team.ru/tracker/api/).

## Install

```bash
npm install st-client --registry=http://npm.yandex-team.ru
```

## Usage

```js
var client = require('st-client').init({ token: '<token>' });

client.getIssue('WEATHER-3300')
  .then(function (issue) {
    console.log('%s – %s', issue.key, issue.summary)
  });

client.issues({ query: 'Queue: WEATHER Key: WEATHER-3300, WEATHER-3301, WEATHER-3302' })
  .then(function (issues) {
    issues.forEach(function (issue) {
      console.log('[%s] %s – %s', issue.status.key, issue.key, issue.summary);
    })
  });
```

## API

### init(options)

Создает клиента.

#### options

Объект с опциями

##### options.token

Type: `String`

OAuth токен. Подробнее в [вики](https://wiki.yandex-team.ru/tracker/api/#avtorizacija).

##### options.sessionId

Type: `String`

Значение куки Session_id. Подробнее в [вики](https://wiki.yandex-team.ru/tracker/api/#avtorizacija).

##### options.tvm

Type: `Object`

Значение сервисного и клиетского  tvm2-тикетов. Объект вида { serviceTicket, clientTicket }. Подробнее в [вики](https://wiki.yandex-team.ru/tracker/api/#avtorizacija).

##### options.lang

Type: `String`
Default: `ru-RU, ru`

Язык. Подробнее в [вики](https://wiki.yandex-team.ru/tracker/api/#lokalizacija).

##### options.endpoint

Type: `String`
Default: `http://st-api.yandex-team.ru/v2`

Адрес API.

##### options.clientOptions

Type: `object`

Опции для [http-клиента got](https://github.com/sindresorhus/got). Позволяют переопределить, например, таймаут или настройки резолвинга.

### Список методов

Методы повторяют структуру API, поэтому описание смотрите на [вики](https://wiki.yandex-team.ru/tracker/api/)

1. [Работа с тикетами](https://wiki.yandex-team.ru/tracker/api/issues/)

    * client.issues([params](https://wiki.yandex-team.ru/tracker/api/issues/list/#primerzaprosa))
    * client.getIssue(id, [params](https://wiki.yandex-team.ru/tracker/api/issues/get/#primerzaprosa))
    * client.createIssue(data)
    * client.updateIssue(id, data)

    1. _Воркфлоу_

        * client.issueTransitions(issueId)
        * client.executeTransition(issueId, transitionId, data)

    1. _[Комментарии](https://wiki.yandex-team.ru/tracker/api/issues/comments/)_

        * client.issueComments(issueId)
        * client.createIssueComment(issueId, data)
        * client.getIssueComment(issueId, commentId)
        * client.updateIssueComment(issueId, commentId, data)
        * client.deleteIssueComment(issueId, commentId)

    1. _[Связи](https://wiki.yandex-team.ru/tracker/api/issues/links/)_

        * client.issueLinks(issueId)
        * client.createIssueLink(issueId, data)
        * client.getIssueLink(issueId, linkId)
        * client.updateIssueLink(issueId, linkId, data)
        * client.deleteIssueLink(issueId, linkId)

    1. _[Связи с удаленными сервисами](https://wiki.yandex-team.ru/tracker/api/issues/remotelinks/)_

        * client.issueRemoteLinks(issueId)
        * client.getIssueRemoteLink(issueId, remoteLinkId)
        * client.createIssueRemoteLink(issueId, data)
        * client.deleteIssueRemoteLink(issueId, remoteLinkId)

    1. _[Аттачи](https://wiki.yandex-team.ru/tracker/api/attachments/)_

        * client.uploadAttachment(data, [query](https://wiki.yandex-team.ru/tracker/api/attachments/upload/#primerzaprosa))
        * client.downloadAttachment(issueId, attachmentId, attachmentName)
        * client.issueAttachments(issueId)

    1. _[История изменений](https://wiki.yandex-team.ru/tracker/api/issues/changelog)_

        * client.issueChangelog(issueId, [params](https://wiki.yandex-team.ru/tracker/api/issues/changelog/#primerzaprosa))

1. Аттрибуты тикета

    1. _[Типы тикетов](https://wiki.yandex-team.ru/tracker/api/types/)_

        * client.issueTypes()
        * client.getIssueType(id)
        * client.createIssueType(data)
        * client.updateIssueType(id, data)

    1. _[Приоритеты](https://wiki.yandex-team.ru/tracker/api/priorities/)_

        * client.priorities()
        * client.getPriority(id)
        * client.createPriority(data)
        * client.updatePriority(id, data)

    1. _[Статусы](https://wiki.yandex-team.ru/tracker/api/statuses/)_

        * client.statuses()
        * client.getStatus(id)
        * client.createStatus(data)
        * client.updateStatus(id, data)

    1. _[Резолюции](https://wiki.yandex-team.ru/tracker/api/resolutions/)_

        * client.resolutions()
        * client.getResolution(id)
        * client.createResolution(data)
        * client.updateResolution(id, data)

    1. _Пользователи_
        * client.users()
        * client.getUser(login)

1. [Работа с очередями](https://wiki.yandex-team.ru/tracker/api/queues/)

    * client.queues([params](https://wiki.yandex-team.ru/tracker/api/queues/list/#primerzaprosa))
    * client.getQueue(id, [params](https://wiki.yandex-team.ru/tracker/api/queues/get/#primerzaprosa))
    * client.createQueue(data)
    * client.updateQueue(id, data)
    * client.deleteQueue(id)

    1. _Атрибуты очереди_

        * client.queueComponents(queueId)
        * client.queueVersions(queueId)
        * client.queueProjects(queueId)

1. [Работа с досками](https://wiki.yandex-team.ru/tracker/api/boards/)

    * client.getBoard(id)

    1. _Спринты_

        * client.boardSprints(boardId)

## Contribution

Пожалуйста, прочитайте [contribution guide](/CONTRIBUTING.md) перед созданием issue или отправкой пулл-реквеста.

## Tests

```
$ npm run lint
$ npm test
```
