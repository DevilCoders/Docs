[![oko health](https://oko.yandex-team.ru/badges/repo.svg?repoName=yandex360/frontend/services/quinn&vcs=arc)](https://oko.yandex-team.ru/arc/yandex360/frontend/services/quinn)
[![oko health](https://oko.yandex-team.ru/badges/repoSecurity.svg?repoName=yandex360/frontend/services/quinn&vcs=arc)](https://oko.yandex-team.ru/arc/yandex360/frontend/services/quinn)

# Quinn

Репозиторий интерфейса https://mail.yandex.ru/touch/
> Quinn Morgendorffer is a fictional character on the MTV animated series Daria.

https://st.yandex-team.ru/QUINN

![QUINN](https://jing.yandex-team.ru/files/yeee737/quinn.png)

## Разработка

Как развернуть на qyp.
[Следовать инструкциям, как завести и настроить машинку](../../tools/qyp#инструкция)
Зайти на свою машинку.

```sh
cd ~/arcadia/yandex360/services/quinn
npm run prepare-dev
```

Если не требуется разработка `homer` или `web-api`, их запускать не нужно, тогда запросы проксируются в актуальную версию Гомера/вебапи (см. https://wiki.yandex-team.ru/pochta/frontend-dev/qyp/#m-kakrabotajutzaglushkii), то есть достаточно запустить тачевый webpack и server:

```sh
cd ~/arcadia/yandex360/services/quinn
npm start
```

`npm run dev` запускает сборку в watch-режиме для русского языка. Если нужна сборка другого или нескольких,
можно указать их: `LANGS=ru,en npm run dev`.

или пользоваться process-manager'ом (например, [overmind](https://github.com/DarthSim/overmind))

```sh
cp Procfile.example Procfile
overmind start
```

Если требуется разработка [web-api](../web-api):

```sh
cd ~/www/services/web-api
npm install
npm start
```

Доступ по url `https://<login>.verstka-dev.mail.yandex.ru/touch`

Если на предыдущих шагах заменить папку `~/www` на `~/<anyname>`, доступ будет по адресу
`https://<login>-<anyname>.verstka-dev.mail.yandex.ru/touch`.

### Разработка корпа

Запуск корпа: `npm run start-corp`. Если нужен нестандартный `web-api`, он запускается `npm run start-corp`, аналогично, если не запускать, используется общая актуальная версия.

Можно overmind'ом:

```sh
cp Procfile.corp.example Procfile
overmind start
```
----

## Гайды

* [Инструкция по сборке проекта](./docs/package.md)
* [Мониторинги](./links.md#Мониторинги)
* [Логи](./logs.md)
* [Локализации](./logs.md)
* [Codestyle](./codestyle.md)
* [Cекреты](./secrets.md)
* [Workflow](./workflow.md)
