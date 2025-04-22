# Фронтенд сервиса Гараж

## Хосты
### dev

http://ytmp-stage2.inno.co

Сервер inno.co (gitlub-ci)

### test

https://garage.taxi.tst.yandex.net/

[Тестовое окружение в Облаке](https://console.cloud.yandex.ru/folders/b1gl52jb8rb9fvlkr037)

### prod

https://garage.yandex

[Продовое окружение в Облаке](https://console.cloud.yandex.ru/folders/b1g6gho40bhgisou1h6p)

## Подготовка
Для работы потребуется Node.js 14.

Для локальной разработки мы используем [NVM](https://github.com/nvm-sh/nvm).

Устанавливаем NVM, а затем:
```bash
# Устанавливаем Node.js 14 версии
nvm install 14

# Переключаемся на эту версию
nvm use 14
```

## Настройка проекта

```bash
# установить зависимости
npm ci
```

## Запуск

```bash
npm start
```

Смотреть после запуска тут: [http://localhost:3000/](http://localhost:3000/).

## Deploy

Для начала нужно:
- [установить CLI yc](https://cloud.yandex.ru/docs/cli/operations/install-cli) (профиль по этой инструкции создавать не нужно);
- [установить Colima](https://github.com/abiosoft/colima) (и установить по инструкции Docker). Нужно будет запускать Colima в дальнейшем для создания Docker контейнера;

### Как достать базовый образ для Облака

Попросить менеджера проекта запросить доступ к базовому образу через тикет в очереди TAXIADMIN.

Пример тикета: https://st.yandex-team.ru/TAXIADMIN-26014

После получения прав:
```bash
# логинимся в федерацию с доступом в облако с базовым образом
yc init --federation-id=ajesnqgjakesl1dvjh47

# конфигурируем Docker для использования docker-credential-yc
yc container registry configure-docker

# выкачиваем базовый образ на локальную машину
docker pull cr.yandex/crpjnf40unocamomb3i5/taxi-base-kube-xenial:latest
```

Подробнее: https://wiki.yandex-team.ru/users/nikkraev/bazovyjj-obraz-vo-vneshnem-oblake/#polucheniebazovogoobraza

### Как залогинится в Облаке проекта

Делаем по аналогии с предыдущим пунктом (см. подробнее).

```bash
# логинимся в федерацию с доступом в облако taxi-outsource-marketplace (перезаписываем профиль с новыми настройками)
yc init --federation-id=ajeefrm3um7gnk7gvaab

# конфигурируем Docker для использования docker-credential-yc
yc container registry configure-docker
```

### Как добавить учетные данные кластеров Kubernetes в конфигурационный файл kubectl
```bash
# Добавляем данные testing кластера
yc managed-kubernetes cluster get-credentials taxi-outsource-marketplace-testing-kubernets-cluster --external --folder-name=testing

# Добавляем данные stable кластера
yc managed-kubernetes cluster get-credentials taxi-outsource-marketplace-stable-kubernets-cluster --external --folder-name=stable
```

### Сборка для kubernetes

Создаем новую ветку и делаем релиз:
- **Бампаем версию в `package.json` и `package-lock.json`**. Увеличиваем минорную версию на 1 (`0.1.0 -> 0.2.0`), в случае хотфикса увеличиваем патч (`0.1.0 -> 0.1.1`).
- **Бампаем версии образов в конфигах kubernetes**:
    * [testing front](kubernetes/testing/drivers-front.deployment.yaml#L17),
    * [testing backoffice](kubernetes/testing/drivers-backoffice.deployment.yaml#L17),
    * [production front](kubernetes/production/drivers-front.deployment.yaml#L17),
    * [production backoffice](kubernetes/production/drivers-backoffice.deployment.yaml#L17).

Мержим ветку в trunk (публикуем PR и получаем approve), а затем:
```bash
# Подтягиваем изменения в trunk
arc checkout trunk
arc pull
```

Следуем дальнейшим инструкциям.

### Как выкатываться в тестинг

[Тестовое окружение в Облаке](https://console.cloud.yandex.ru/folders/b1gl52jb8rb9fvlkr037)

Поменять кластер в kubectl конфиге на testing:
```bash
kubectl config use-context yc-taxi-outsource-marketplace-testing-kubernets-cluster
```

Перейти в папку testing:
```bash
cd kubernetes/testing/
```

Собрать и загрузить образ в Docker registry в тестовом окружении:
```bash
make all_push
```

Выкатить новую версию в тестинг:
```bash
make all_deploy
```

### Как выкатываться в production

[Продовое окружение в Облаке](https://console.cloud.yandex.ru/folders/b1g6gho40bhgisou1h6p)

Поменять кластер в kubectl конфиге на stable:
```bash
kubectl config use-context yc-taxi-outsource-marketplace-stable-kubernets-cluster
```

Перейти в папку production:
```bash
cd kubernetes/production/
```

Собрать и загрузить образ в Docker registry в продовом окружении:
```bash
make all_push
```

Выкатить новую версию в прод:
```bash
make all_deploy
```

### Как откатить релиз

Меняем вручную версию образа в конфигах kubernetes интересующего окружения:
- [testing front](kubernetes/testing/drivers-front.deployment.yaml#L17),
- [testing backoffice](kubernetes/testing/drivers-backoffice.deployment.yaml#L17),
- [production front](kubernetes/production/drivers-front.deployment.yaml#L17),
- [production backoffice](kubernetes/production/drivers-backoffice.deployment.yaml#L17).

Выкладываем в trunk и выкатываем в окружение.

### Полезные команды
`kubectl get pods` — при помощи этой  команды можно посмотреть информацию по каждому из подов. В зависимости от выбранного кластера в kubectl конфиге будут показаны поды stable или testing.

### Известные проблемы
Если возникают проблемы с доступом к базовому Docker образу, на операцию push в облако taxi-outsource-marketplace или еще какому-либо доступу, то следует проверить в нужной ли федерации произведен вход — что для 1-го, что для 2-го доступа нужны разные федерации.
