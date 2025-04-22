# Локальная отладка сервисов с TVM

Для того чтобы сходить в API, закрытое TVM, понадобится утилита `tvmknife`.  
Проще всего её получить через [ya tool](https://docs.yandex-team.ru/devtools/intro/quick-start-guide#ya-setup).

### Как узнать TVM id сервиса в Shiva
Для сервисов, живущих в шиве, TVM-приложения генерятся [автоматически](https://docs.yandex-team.ru/classifieds-infra/auto#tvm-resurs).  
Секрет и TVM id будут доступны владельцам сервиса в [секретнице](https://yav.yandex-team.ru/?search=autogen-tvm). Найти можно поиском по `autogen-tvm.[TEST|PROD].<имя-сервиса-в-карте>`.  
Если хочется узнать TVM id чужого приложения, можно поискать по [ресурсам](https://abc.yandex-team.ru/services/verticals/resources/?view=consuming&layout=table&supplier=14&type=47) в ABC Сервисы Вертикалей.


### Сходить в API, закрытое UserTicket'ами

UserTicket можно получить:
- в обмен на ssh-ключ разработчика (только в yandex-team), указав TVM id приложения:
```bash
ya tool tvmknife get_user_ticket sshkey --tvm_id 100500
```
- в обмен на OAuth-токен разработчика.  
Быстро получить OAuth-токен на 24 часа можно по [ссылке](https://oauth.yandex-team.ru/authorize?response_type=token&client_id=6a6b2642d15e49e4b5720158bb67165a).
```bash
ya tool tvmknife get_user_ticket oauth --tvm_id 100500 -b blackbox.yandex-team.ru
```

Полученный тикет нужно передать в заголовке `X-Ya-User-Ticket`.


{% note warning %}

Выписать UserTicket для внешнего [blackbox](https://docs.yandex-team.ru/blackbox/concepts/location) с локальной тачки не получится – нужны дырки.

{% endnote %}

### Сходить в API, закрытое ServiceTicket'ами

ServiceTicket можно получить:
- в обмен на ssh-ключ разработчика, но нужно будет получить роль **TVM ssh пользователь** в ABC своего сервиса.  
Автосгенеренные шивой TVM-приложения живут в ABC [Сервисы Вертикалей](https://abc.yandex-team.ru/services/verticals/resources/?view=consuming&layout=table&supplier=14&type=47). Если это ваш случай, роль можно запросить по [ссылке](https://idm.yandex-team.ru/#rf-role=fRHejUPQ#abc/services/verticals/*/631(fields:()),rf-expanded=fRHejUPQ,rf=1).
```bash
ya tool tvmknife get_service_ticket sshkey --src 100500 --dst 100501
```
- в обмен на секрет приложения. В случае автогенерации секрет будет лежать в [секретнице](https://yav.yandex-team.ru/?search=autogen-tvm).
```
ya tool tvmknife get_service_ticket client_credentials --src 100500 --dst 100501
```

Полученный тикет нужно передать в заголовке `X-Ya-Service-Ticket`.

## Полезные ссылки

[Документация TVM](https://wiki.yandex-team.ru/passport/tvm2)
