> ⚠️ Не поддерживается: https://clubs.at.yandex-team.ru/devtools-frontend/586

# arctic-husky

**arc**tic [husky](https://github.com/typicode/husky) 🐶

![huskies](https://jing.yandex-team.ru/files/juliethefox/uhura_2020-05-13T12%3A45%3A06.795957.jpg)

Инструмент для работы с [хуками Arc VCS](https://doc.yandex-team.ru/arc/manual/arc/hooks.html).

Функциональность аналогична [`husky`](https://github.com/typicode/husky) для git-репозиториев.

Внутри использует форк [`@yandex-int/husky`](https://gitlab.yandex-team.ru/search-interfaces/husky/).

## Назначение инструмента

Конфигурация хуков в arc хранится локально и не коммитится в репозиторий.
Таким образом, каждый разработчик должен сам предварительно сконфигурировать хуки.
Пакет позволяет описывать вызывающиеся в хуках скрипты в файлах конфигурации в репозитории, и автоматически конфигурировать их на локальной машине при установке пакета.

## Установка хуков

```shell
npm install --save --registry=https://npm.yandex-team.ru/ @yandex-int/si.ci.arctic-husky
```

В момент установки пакета в `.arcconfig` будут прописаны скрипты, вызывающие в свою очередь пользовательские скрипты хуков, описанные в вашем package.json или `.huskyrc.json`.
Подробнее – в документации [husky](https://github.com/typicode/husky#install), формат и возможности конфигурации полностью совпадают.

Хуки будут прописаны для той директории, в которой выполнялась установка пакета.
