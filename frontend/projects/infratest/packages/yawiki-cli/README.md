# Yandex Wiki API Command Line Client

CLI для [Yandex Wiki REST API](https://wiki.yandex-team.ru/wiki/dev/api/autodocs/).

## Установка

```shell
npm install --save --registry=https://npm.yandex-team.ru/ @yandex-int/si.ci.yawiki-cli
```

## Требования

`yawiki` требует OAuth-токен для авторизации, который ожидается в переменной окружения `YAWIKI_OAUTH_TOKEN`.

## Использование

```shell
yawiki has-page path/to/page

yawiki load-page path/to/page --format=raw
yawiki load-page path/to/page --format=html

yawiki create-page path/to/page --content=path/to/file.raw --title="<title>"
yawiki create-page path/to/page --content-template=template.ejs --content-data=data.json --title="<title>"

yawiki update-page path/to/page --content=path/to/file.raw --title="<title>"
yawiki update-page path/to/page --content-template=template.ejs --content-data=data.json --title="<title>"
```
