## Общее описание

В этом каталоге содержатся вспомогательные файлы для сборки и загрузки образов
компонентов проекта во внешнее Яндекс.Облако.
В документе описывается что и как там работает, что нужно сделать для того,
чтобы обновить образ.

## Аутентификация в федерации

[Установка CLI yc](https://cloud.yandex.ru/docs/cli/operations/install-cli)

Федерация проекта: `ajeefrm3um7gnk7gvaab`
URL федерации: <https://console.cloud.yandex.ru/federations/ajeefrm3um7gnk7gvaab>

```
yc init --federation-id=ajeefrm3um7gnk7gvaab
```

## Как выкатываться в тестинг

[Тестовое окружение в Облаке](https://console.cloud.yandex.ru/folders/b1gl52jb8rb9fvlkr037)

```shell
cd kubernetes/testing/
```

Собрать из загрузить образ в Docker registry в тестовом окружении

```shell
make all_push
```

Выкатить новую версию в тестинг

```shell
make all_deploy
```

## Как выкатываться в стейбл

[Продовое окружение в Облаке](https://console.cloud.yandex.ru/folders/b1g6gho40bhgisou1h6p)

```shell
cd kubernetes/stable/
```

Собрать из загрузить образ в Docker registry в тестовом окружении

```shell
make all_push
```

Выкатить новую версию в тестинг

```shell
make all_deploy
```