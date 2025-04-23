# Задача

Нужно удалять доверенные контакты при удалении юзера через админку. \
Тикет: [TAXIBACKEND-27578](https://st.yandex-team.ru/TAXIBACKEND-27578)

Автор задачи сказал, что если сохранение контактов на полгода сильно
трудозатратнее, то можно удалять контакты сразу (в любом случае юзеры сами
могут править нашу базу, мы не сохраняем нигде удаленные пользователями
контакты). \
Поэтому делаем простой вариант (без отсрочки удаления).

# Реализация

## Общий план (детали см. ниже)

Создаем новую ручку в `safety-center`, которая будет удалять контакты
пользователя из базы ЦБ. \
Создаем api-proxy ручку, которая объединит ручку `/api/user_info/delete_user/`
из старого бэка и новую. \
Используя админку без кода, создаем адрес для похода в api-proxy с проверкой
admin_permissions. \
Убираем проверку прав в старом бэке.

\+ к основному плану есть доработка. \
Заметили, что в `/4.0/safety_center/v1/contacts` контакты достаются только
по yandex_uid из хедера (не учитываются `X-YaTaxi-Bound-Uids`).
Надо их тоже доставать и, соответственно, удалять. \
UPD: поняли, что быстро это исправить сложно. Не столько потому, что много
править, сколько потому, что нужно более детально заняться этим вопросом, так
как непонятно, в каких местах еще не обрабатываются связанные uid. \
На данный момент выявили две возможные проблемы. \
1) Есть ограничение на количество контактов SAFETY_CENTER_MAX_CONTACTS. Это
может помешать смерджить, как это планировалось, списки контактов со связанных
аккаунтов.
1) Возможно, будет проблема с непосредственно отправкой смс этим доверенным
контактам (может не всем, кого будет видно, отправиться или отправиться дважды
из-за того, что один и тот же контакт есть в нескольких списках и т. п.).

Так как это не входит в задачу, решили просто создать отдельный тикет на
проработку/доработку - [TAXIBACKEND-28839](https://st.yandex-team.ru/TAXIBACKEND-28839)

## safety-center

### Создаем ручку POST `/safety-center/v1/delete-user`
Принимает в запросе phone и phone_type. \
Отвечает 200.
1. Достаем с помощью ручки `user-api` `/user_phones/by_number/retrieve` \
phone_id по phone и phone_type.
1. Достаем с помощью ручки `zalogin` `zalogin/v1/internal/phone-info` все связанные uid
по phone_id (новая ручка - [тикет](https://st.yandex-team.ru/TAXIDATA-2306)).
1. Для всех уидов из полученного списка удаляем их контакты, если они есть в базе.

## api-proxy
Создаем ручку `/v1/delete-user` с POST методом, объединяющую
`/api/user_info/delete_user` и `/v1/delete-user`. \
Принимает телефон, тип телефона и тикет. \
Не требуем авторизации (отключаем от PA).

Добавляем два новых ресурса:
- `api-user-info-delete-user` -> POST `/api/user_info/delete_user/`
- `safety-center-v1-delete-user` -> POST `/v1/delete-user`

```yaml
default-response: resp-ok
allow-unauthorized: true
sources:
  - id: py2-delete-user
    resource: api-user-info-delete-user
    body#object:
      - key: phone
        value#xget: /request/body/phone
      - key: phone_type
        value#xget: /request/body/phone_type
      - key: ticket
        value#xget: /request/body/ticket

  - id: safety-center-delete-user
    resource: safety-center-v1-delete-user
    body#object:
      - key: phone
        value#xget: /request/body/phone
      - key: phone_type
        value#xget: /request/body/phone_type
responses:
  - id: resp-ok
enabled: true
```

## taxi-api-admin
Создаем новый файл `api-proxy-handlers.yaml`.
```yaml
tvm_auth:
    service_name: api-proxy

hosts:
    unstable: http://api-proxy.taxi.dev.yandex.net
    testing: http://api-proxy.taxi.tst.yandex.net
    production: http://api-proxy.taxi.yandex.net

api:
  - path: v1/delete-user/
    methods:
      - method: post
        permissions:
          - delete_user
        audit_action_id: delete_user

audit_actions:
admin_permissions:
```

## backend
Кажется, надо убрать только проверку permission, но, возможно, нужно будет
поправить что-то еще (возможно, аудирование и какие-то другие детали не из
основной логики), поэтому заложу побольше.

## фронт
Как только будет точно понятно API api-proxy, можно будет с ними договориться
о смене урла (со старого бэка на api-proxy) и заводить им доработку. В оценке
по времени их работу учитывать не буду, так как 1) не могу оценить их объем
работы; 2) они не блочат разработку на бэке.

## Оценка по времени
[1d] Написание ручки `/safety-center/v1/delete-user`. \
[1d] api-proxy \
[1d] АБК \
[1d] backend. \
[1d] Проверка в тестинге + багфиксы по результатам. \
[2d] Время, которое уйдет на ревью ПРов (которое не войдет в промежутки,
описанные выше) + время на выкатки сервисов

**Итого: 7d**

