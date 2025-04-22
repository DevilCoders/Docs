# Выкладка и откат релизов в Deploy

В штатном режиме релизы и хотфиксы собираются средствами NewCI: [подробная документация](../../guide/releases/release-newci)

Однако есть две внештатных ситации, требующих ручных действий: откат релиза и поломка флоу NewCI.

## Как откатить 

Чтобы откатить нужно выбрать предыдущую конфигурацию и применить её.

1. Переходим на вкладку `History`
2. Выбираем предыдущую ревизию (комментарий будет примерно такой: "CI autocommit: Release: Release %appname% to Yandex Deploy #%version%")
3. Нажимаем `Apply`, дальше `Apply as is`
4. Откроется diff, в котором можно дописать комментарий к релизу, нажимаем Deploy. Если настроена полокационная выкатка, то будет доступна вторая кнопка "Ignore per location and Deploy". Она предпочтительная для более быстрого отката.

{% cut "Скриншот" %}

![stage history](_assets/stage_history.png "Откат на предыдущую ревизию")

{% endcut %}

{% cut "Скриншот" %}

![ignore per location and deploy](_assets/revert_with_ignore_per_location.png "Деплой с игнорированием полокационности" =372x105)

{% endcut %}


## Выкладка вручную

1. Написать в чате [Direct.Admin.Chat]({{chat-direct-admin}}), что собираешь выложить релиз.
2. Из релизного тикета взять версию сервиса
3. Найти в [Сандбоксе](https://sandbox.yandex-team.ru) таску, в которой собрана релизная версия. Её мог оставить в комментарии релиз инженер. Либо найти самому: искать задачу DIRECT_YA_PACKAGE + версию в описании, [пример (версию подставить из релиза)](https://sandbox.yandex-team.ru/tasks?children=true&desc_re=1.7333041-1&type=DIRECT_YA_PACKAGE&limit=20&created=14_days). Если до этого был запущен флоу в NewCI, ссылку можно взять на кубике Build package 

{% cut "Скриншот" %}

![build package](_assets/build_package_in_newci.png "Ссылка на таску сборки релизной версии"  =200x198)

{% endcut %}

4. Зарелизить ресурс в Сандбоксе: кнопки Release, subject Stable.

   {% note info "Если не хватило прав, выполни на ppcdev:" %}

   ```sh
   SANDBOX_TOKEN_FILE=/etc/direct-tokens/sandbox_oauth_token_ppc dt-sandbox-resource-release.py -s stable -t <id таски>
   ```

   {% endnote %}
5. Дождаться, что таска в Сандбоксе перейдет в состояние Released Stable (зеленая бирка в шапке)
6. Пойти в интерфейс ЯДеплоя, на вкладку Deploy tickets продакшенового стейджа: [logviewer](https://deploy.yandex-team.ru/stages/direct-logviewer-production/deploy-tickets), [canvas](https://deploy.yandex-team.ru/stages/direct-canvas-production/deploy-tickets), [java-intapi](https://deploy.yandex-team.ru/stages/direct-intapi-production/deploy-tickets), [java-web](https://deploy.yandex-team.ru/stages/direct-java-web-production/deploy-tickets), [ess-router](https://deploy.yandex-team.ru/stages/direct-java-ess-router-production/deploy-tickets), [oneshot](https://deploy.yandex-team.ru/stages/direct-java-oneshot-production/deploy-tickets), [java-api5](https://deploy.yandex-team.ru/stages/direct-java-api5-production/deploy-tickets), [java-jobs](https://deploy.yandex-team.ru/stages/direct-java-jobs-production/deploy-tickets), [java-alw](https://deploy.yandex-team.ru/stages/direct-java-alw-production/deploy-tickets)
7. Найти деплойный тикет с таской из п.2 (Обычно он там один)
8. Нажать на деплойном тикете Commit
9. В случае java-web/java-api/java-intapi выкладка пойдет полокационно в порядке VLA, затем IVA, затем SAS. При этом на одной локации раскатится автоматически, для продолжения деплоя необходимо нажать аппрув на следующей локации(ограничение только для одной, но следующая за ней ждет ее), посмотрев состояние сервиса. Если проблемы будут заметны на одном ДЦ, можно откатить релиз, попутно закрыв, выкрутив вес в 0, проблемную локацию через L7-heavy интерфейс: ссылки на секции для наших балансеров [web](https://nanny.yandex-team.ru/ui/#/l7heavy/direct.yandex.ru/) [api](https://nanny.yandex-team.ru/ui/#/l7heavy/api.direct.yandex.ru/) [intapi](https://nanny.yandex-team.ru/ui/#/l7heavy/intapi.direct.yandex.ru/) по инструкции [закрытия локации через L7](../../jeri/howto-dc-l7.md)
10. Дождаться применения патча
11. (Опционально) нажать на ненужных тикетах Skip (Как это делать эффективно и не терять нужные тикеты?)

## Если не работает
Логи льются в логвьювер. Их можно найти по сервису или по FQDN. [Пример фильтра](https://direct.yandex.ru/logviewer/short/FgCzdbwr3jdjB7)

Если даже логи не добегают, то если разкрыть параметры конкретного пода, будет отображаться строка подключения по ssh.

## Ссылки

- [Релизы и хотфиксы в NewCI](../../guide/releases/release-newci)
- [Документация на релизные правила в ЯДеплое](https://wiki.yandex-team.ru/deploy/docs/concepts/release-integration/)



