# Crossplane 1.6.1 с поддержкой Yandex Cloud

[Crossplane](https://crossplane.io) - дополнение к Kubernetes с открытым исходным кодом, который позволяет командам
разработки платформы собрать инфраструктуру для несколькьких вендоров, и производить более высокоуровневые API сервисов
для потребления командами разработки приложений.

**Инструкция по развертыванию**

1. Откройте [консоль управления](https://console.cloud.yandex.ru/) and select the Kubernetes cluster.
2. Перейдите на вкладку **Marketplace**.
3. Выберите продукт **Crossplane**.
4. Нажмите кнопку **Использовать**.
5. Нажмите кнопку **Установить**.
6. Создайте сервисный аккаунт [через консоль управления](https://cloud.yandex.com/ru/docs/iam/operations/sa/create),
   либо через CLI:

```
yc iam service-account create --name crossplane --folder-id <FOLDER_ID>
```

7. Назначьте сервисному аккаунту
   роль `admin` [через UI](https://cloud.yandex.ru/docs/iam/operations/sa/assign-role-for-sa) или через CLI:

```
yc resource-manager folder add-access-binding <FOLDER_ID> --role admin --subject serviceAccount:<SERVICE_ACCOUNT_ID>
```

8. Создайте авторизованный ключ для сервисного аккаунта через cli и скопируйте полученный на экране вывод:

```
yc iam key create --service-account-id <SERVICE_ACCOUNT_ID> --output sa-key.json && tr -d '\n' < sa-key.json
```

9. Создайте секрет в kubernetes с ключем сервис аккаунта:

```
kubectl create secret generic yc-creds -n "crossplane-system" --from-file=credentials=./sa-key.json
```

10. Примените ProviderConfig:

```
kubectl apply -f https://raw.githubusercontent.com/yandex-cloud/provider-jet-yc/main/examples/providerconfig/providerconfig.yaml
```

## Примеры использования

* Управление облачными ресурсами через Kubernetes.
* Управление multi-cloud инфраструктурой.

## Полезные ссылки

[Документация](https://crossplane.io/docs/)<br/>

## Техническая поддержка

Служба технической поддержки Yandex.Cloud отвечает на запросы 24 часа в сутки, 7 дней в неделю. Доступные виды запросов
и срок их обработки зависят от тарифного плана. Подключить платную поддержку можно
в [консоли управления](https://console.cloud.yandex.ru/support?section=plan). Подробнее о порядке
оказания [технической поддержки](https://cloud.yandex.ru/docs/support/overview). Вы также можете воспользоваться
помощью [сообщества](https://www.vaultproject.io/community).

## Лицензионное соглашение

Используя данный продукт, вы соглашаетесь
с [Условиями использования Yandex Cloud Marketplace](https://yandex.ru/legal/cloud_terms_marketplace/) и с условиями
использования следующих
продуктов: [Crossplane provider-jet-yc](https://github.com/yandex-cloud/provider-jet-yc/blob/main/LICENSE)
, [Crossplane](https://github.com/crossplane/crossplane/blob/master/LICENSE).
