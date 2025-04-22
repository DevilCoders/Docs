# Developing of DOCS

## Как проверить локально?

В корне выполнить `make docs`.

Откроется браузер с локально собранной документацией.

## Как добавить новый раздел?

- Создать Markdown файл в нужном месте
- Указать её в [`toc.yaml`](https://docs.yandex-team.ru/docstools/settings/toc)

  ```
  items:
    - name: Your title
      href: relative/to-markdown-file.md
  ```
