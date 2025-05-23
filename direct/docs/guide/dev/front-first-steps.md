# Первые шаги для фронтенд-разработчика Директа

## Подписаться на рассылки QA

Для того чтобы быть в курсе событий рекомендуется подписаться на рассылки
через [интерфейс ml](https://ml.yandex-team.ru/):

* Только для сотрудников Директа: разработка и управление проектами [direct-team](https://ml.yandex-team.ru/lists/direct-team/)
* Для рабочего разруливания верстальных проблем [verstka](https://ml.yandex-team.ru/lists/verstka/)

При желании можно подписаться на любые другие рассылки по интересующей тематике.

## Чаты

Вступить в чаты:

- [Чат фронтенда](https://t.me/joinchat/TrHQwTqlZ4pmM2Y6)
- [Чат про проблемы с тестами](https://t.me/joinchat/HVT4xMSRmRp5AORs)

Попросите руководителя или курирующего ментора, чтобы вас добавили во все релевантные чаты и каналы, не упомянутые здесь. Или добавьтесь самостоятельно, если вы знаете, куда, с помощью [страницы со списком чатов](../../reference/chats)

## Установить необходимые приложения и инструменты

Установить через Self-Service (предустановлен на маках)

- iTerm2
- WebStorm
- Cisco Proximity

Также, необходимо установить:

- [Яндекс Браузер](https://browser.yandex.ru/) - рекомендуемый браузер для разраоботки
- [Homebrew](https://brew.sh/index_ru) - менеджер пакетов приложений для macOs

## Сгенерировать и разложить ssh-ключи

[Инструкция по настройке ssh](../../dev/ssh)

## Запросить роли в сервисах

Для фронтенд-разработчика разработчика чаще всего нужна роль Разработчик в проде и Суперпользователь на тестовых средах.

[Инструкция по получению ролей](../qa/qa_kmb/qa_roles#create-roles)

## Установить общеяндексовые инструменты для разработки

Система контроля версии `arc`, утилита `ya`.

- [Установить утилиты и прочитайте общую документацию по разработке](https://docs.yandex-team.ru/devtools/intro/quick-start-guide)
- Примонтировать единый репозиторий в директорию `~/arcadia`

## Зарезервировать для себя беты

Для разработки бывает нужно создавать отдельные экземпляры Директа, на которых удобно отлаживать и проверять свой код.
Стоит узнать у руководителя на каком [ppcdev](../../glossary/glossary#ppcdev) лучше
создавать [беты](../../glossary/glossary#beta) и зарезервировать по инструкции.

[Инструкция по резервированию портов на бете](../../dev/betas/betas#beta-ports)

## Установить Node Version Manager

Для удобства разработки необходимо установить менеджер версий Node.js®.

Если не существует файл, то создать: `~/.profile`, а затем выполнить

```(bash)
curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.31.0/install.sh | bash
source ~/.nvm/nvm.sh
```

Рабочие версии строго зафиксированы в целях стабильности работы, следует указать их явно:

```(bash)
nvm install 16.13.2
nvm use alias default 16.13.2
npm install --registry=https://npm.yandex-team.ru --global pnpm@6.32.3
```
