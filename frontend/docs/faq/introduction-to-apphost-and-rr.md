# Как работает стэк Apphost + Report Renderer?
Очень абстрактно разберем, как обрабатывается запрос юзера, в контексте стэка под Apphost и Report Renderer.

1. Вводим в браузере `yandex.ru/test` и жмем Enter.
2. Попадаем на [L7](https://wiki.yandex-team.ru/L7/), главный балансер Яндекса.
3. Внутри балансера ([L7](https://wiki.yandex-team.ru/L7/)) прописано, что по урлу `/test` надо пойти в apphost. [Пример конфига балансера](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/ugc.search.yandex.net/upstreams/list/ugcpub-ugc-pages_https/show/)
4. Запрос попадает в apphost.
5. Перед apphost есть специальный сервис – http_adapter. Этот сервис соотносит урл `/test` с графом который нужно вызвать.  [Конфиг http_adapter для грибов](https://a.yandex-team.ru/arc/trunk/arcadia/apphost/conf/verticals/SHARED/_routing_config.json)
6. Далее отрабатывает apphost по нужному графу для вашего сервиса. [Граф сервиса ugc](https://horizon.z.yandex-team.ru/graphs/SHARED/ugcpub_cabinet/6258854)
7. Самая важная для нас часть этого графа - это источник TEMPLATES, он же Report Renderer. В графе где есть Report Renderer, будет такой кусок:
```
"TEMPLATES_SETUP": {
      "embed": {
          "type": "template_params",
          "template": "ugcpub"
      }
}
```
Свойство `template` это id шаблона, который будет использован для рендера сервиса по урлу `/test`.
Также в графе видно сам сервис Report Renderer:
```
"TEMPLATES": {
      "source": "RENDERER_SHARED",
      "balancing_scheme": "rrobin",
      "timeout": "1s"
}
```
Источник `RENDERER_SHARED` - это кластер Report Renderer для сервисов которые живут в вертикали `SHARED`. [ссылка на RENDERER_SHARED в няне](https://nanny.yandex-team.ru/ui/#/services/catalog/renderer_shared_man/files)
8. Дальше Report Renderer запускает шаблон и сохраняет в контекст apphost полученный html. На этом apphost заканчивает обход графа, и отдает наружу html ответ.
9. Пользователь видит страничку, которую отдал наш шаблон.

## Полезные ссылки
- [Официальная документация по apphost](https://doc.yandex-team.ru/apphost/)
- [Документация по Report Renderer](https://wiki.yandex-team.ru/search-interfaces/infra/report-renderer/)
