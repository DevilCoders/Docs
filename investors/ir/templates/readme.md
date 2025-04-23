# ir-template

Благодаря платформе [magicdev](https://github.yandex-team.ru/project-stub/magicdev#Что-это-зачем-и-как-этим-пользоваться), проект разрабатывается локально.

Для работы потребуется _Node.js 8_ – устанавливаем его по необходимости:

```bash
brew install nvm
nvm install 8
```

Далее устанавливаем зависимости и запускаем проект:

```bash
npm run deps

# Magicdev запросит ваш пароль, чтобы запустить на 443 порту
npm run dev
```

Проект становится доступен по адресу:
https://localhost.msup.yandex.com/

## Чтобы собрать html-файл и статику

Необходимо запустить команду

```bash
npm run build:production
```

Необходимые файлы появятся в папке _out_

![](https://jing.yandex-team.ru/files/m-smirnov/ir-template_wwwir-template_-_...static.enbtechspriv-to-bemjson.js_ir-template_2018-02-06_17-19-27.png)
