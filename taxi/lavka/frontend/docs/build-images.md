Обновление build-images
----

Инструкция рассказывает, как использовать специальный релизный флоу [build-images](https://a.yandex-team.ru/projects/lavkafrontend/ci/releases/timeline?dir=taxi%2Flavka%2Ffrontend&id=build-images),
чтобы корректно и без усилий обновить все связанные образы, используемые в ci, sandbox, nanny в проекте Лавки.

На основе базового docker образа обновляются все остальные разом.

### Инструкция
1. Вносим обновления в базовый Dockerfile [вот тут](https://a.yandex-team.ru/projects/lavkafrontend/code/taxi/lavka/frontend/tools/lib/ci/images/docker/baseimage/Dockerfile?rev=r9387045&dir=taxi%2Flavka%2Ffrontend#L12)
2. Если в п.1 внесли изменения в базовый Dockerfile, то коммитим код в trunk, так как релиз build-images будет собираться из trunk
3. Поднимаем ревизию образа [вот тут](https://a.yandex-team.ru/projects/lavkafrontend/code/taxi/lavka/frontend/a.yaml?rev=r9387045&dir=taxi%2Flavka%2Ffrontend#L51)
4. Запускаем
     ```sh
        npm run audit:images
    ```
   - после выполнения релизного флоу новый версии будут опубликованы в комментариях к тикету [LAVKASERVICES-101](https://st.yandex-team.ru/LAVKASERVICES-101)

5. Следуем инструкциям из запущенной команды
6. Обновляем lxc образ sandbox ресурса [вот тут](https://a.yandex-team.ru/projects/lavkafrontend/code/taxi/lavka/frontend/a.yaml?rev=r9387045&dir=taxi%2Flavka%2Ffrontend#L52)

