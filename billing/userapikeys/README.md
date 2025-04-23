# UserApiKeys — внешнее API Кабинета Разработчика

### Сборка

Образа Docker
```
./ya make --checkout -o=billing/userapikeys/build billing/userapikeys
cd billing/userapikeys
docker build -t registry.yandex.net/balance/userapikeys .
```

### Релиз

#### Сборка

* Собрать образ в сандбоксе https://sandbox.yandex-team.ru/task/598348754/view (любые сандбокс-таски, связанные с проектом, стоит обязательно помечать тэгом `YANDEX-BALANCE-USERAPIKEYS`)
* Создать тикет по форме вот этого [APIKEYS-1655](https://st.yandex-team.ru/APIKEYS-1655) и дождаться подтверждения

#### Выкладка

* Вручную переконфигурировать [stage проекта billing-userapikeys деплое](https://deploy.yandex-team.ru/stages/billing-userapikeys-prod-stage), указав новую версию образа и выполнив прочие предписания из тикета, а в сообщении к коммиту приложить ссылку на тикет
* Отписаться в тикете, для верности приложив дифф настроек стейджа
