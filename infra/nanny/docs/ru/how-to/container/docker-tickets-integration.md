# Tickets Integration для Няня-сервисов с Docker Layers

## Создание докер-релиза в Няне {#create-docker-release}

Для того, чтобы оповестить Няню об обновлении докер образа в реждистри, необходимо создать в Няне релиз специального типа  `DOCKER_RELEASE`. Для этого нужно отправить HTTP **POST** запрос `/api/tickets/CreateRelease/` с релизом в теле запроса.

### Пример запроса {#sample}

```json
{
  meta: {
    author: "<username>"
  },
  spec: {
    type: "DOCKER_RELEASE",
    docker_release: {
      "image_name": "foo/bar",
      "image_tag": "v123",
      "release_type": "TESTING"  // STABLE, PRESTABLE, TESTING
    }
  }
}
```

### Создание докер-релиза в Няне через ya package {#create-docker-release-ya-package}

Также докер-релиз в Няне можно создать, используя утилиту `ya package --docker`. Для этого при публикации образа необходимо указать параметр `--nanny-release` с одним из возможных значений `TESTING`, `STABLE`, `PRESTABLE`:

```bash
ya package <package.json> --docker --docker-push --nanny-release TESTING
```
Подробнее про `ya package --docker` [тут](https://wiki.yandex-team.ru/yatool/package/#cborkadocker-obrazov).

## Настройка Tickets Integration {#setup}

Для того, чтобы при появлении в Няне докер-релиза стригерилось обновление соответствующего Няня-сервиса, необходимо настроить для него `Tickets Integration`. Для этого нужно:

1. Включить Tickets Integration для сервиса.

    ![vydelenie004.png](https://jing.yandex-team.ru/files/sshipkov/vydelenie004.5ff48c9.png)

2. В разделе `Docker release rule` заполнить поля, на основе которых будет происходить матчинг докер-релиза и сервиса. При совпадении этих полей с соответствующими полями докер-релиза, для сервиса будет создан тикет на обновление `docker_image` сервиса (см пример ниже):
    * `Which release type to match` имя докер-образа;
    * `Which image name to match` тип докер-релиза (один из `STABLE`, `PRESTABLE`, `TESTING`).

    ![vydelenie003.png](https://jing.yandex-team.ru/files/sshipkov/vydelenie003.7dc5461.png)

3. Указать очередь, в которой нужно создать тикет. Без указания очереди, тикет для сервиса создан не будет.
4. [опционально] Включить автокоммит снэпшота с указанием приоритета вкоммичивания.

### Пример матчинга {#matching-sample}

Допустим для сервиса `S` указано следующее:

* `Which release type to match` `STABLE`
* `Which image name to match` `foo/bar`

Тогда при появлении докер-релиза в Няне, например, со следующим содержимым:

```json
{
  meta: {
    author: "<username>"
  },
  spec: {
    type: "DOCKER_RELEASE",
    docker_release: {
      "image_name": "foo/bar",
      "image_tag": "v123",
      "release_type": "STABLE"
    }
  }
}
```

будет создан тикет, обновляющий `docker_image` сервиса `S` на `"foo/bar:v123"`.
