# Запуск нового сервиса

1. Создаем проект локально. Запускаем команды в корне.
    ```
    npx codegen project new
    make deps
    make ansible-local-configure
    ```

2. Создаем новую release джобу в [TeamCity](https://t.vertis.yandex-team.ru/admin/editProject.html?projectId=vs_frontend_Applications_RealtyNew).
Для этого можно склонировать джобу другого нашего проекта и поправить параметры.

3. В этот [репозиторий](https://github.com/YandexClassifieds/services)
добавляем [карту сервиса](https://github.com/YandexClassifieds/services/tree/master/maps)
и [манифест деплоя](https://github.com/YandexClassifieds/services/tree/master/deploy), 
опять же, копируем один из наших проектов (любой из realty-front-*).

    **Q:** Как выбрать количество инстансов и ресурсов?<br>
    **A:** Перед стартом это сделать сложно, можно поставить - для тестового окружения (test): cpu: 100, memory: 2048, count: 1, для продакшн окружения (prod) cpu: 2000, memory: 2048, count: 5,
    а после запуска посмотреть на реальное потребление и подкрутить.

4. После мержа PR с картой и манифестом, [делегируем](https://wiki.yandex-team.ru/vertis-admin/deploy/secret/#cli-utilita) необходимые секреты.

5. [Деплоем](./deploy.md). Только в тестинг, пока не готовы к запуску наружу.

6. Добавляем нагрузку, для этого нужно завести тикет на админов в очередь VASUP.
Описываем, на каком урле должен жить сервис.

Готово!
