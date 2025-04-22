### Стенды

Сейчас [Yandex Deploy](https://deploy.yandex-team.ru/) есть несколько готовых стендов для бекенд разработчиков:
* стенды для [Вики интранет](https://deploy.yandex-team.ru/projects/wiki-back-stand-intranet) и
* стенды для [Вики B2B](https://deploy.yandex-team.ru/projects/wiki-back-stand-b2b).

У каждого разработчика есть свой стенд: `Stage ID` стенда включает в себя логин разработчика + цифровой идентификатор,
например, `wiki-back-stand-intranet-elisei1`.
Работу сервиса обеспечивают два стенда, отвечающие за фронтенд и АПИ бекенда.

1. Собрать образ и задеплоить на стенд АПИ бекенда для `elisei1`:
* для интранета ([ссылка на стейдж](https://deploy.yandex-team.ru/stage/wiki-back-stand-intranet-elisei1)):
```
    $ make stand-wiki s=elisei1
```

* для B2B ([ссылка на стейдж](https://deploy.yandex-team.ru/stage/wiki-back-stand-b2b-elisei1)):
```
    $ make stand-b2b s=elisei1
```

2. Задеплоить образ (например, версию из тестинга) на стенд фронтенда для `elisei1`:
* для интранета ([ссылка на стейдж](https://deploy.yandex-team.ru/stage/wiki-www-stand-intranet-elisei1)):
```
    $ make deploy-stand-front-wiki s=elisei1 v=10.205.0
```

* для B2B ([ссылка на стейдж](https://deploy.yandex-team.ru/stage/wiki-www-stand-b2b-elisei1)):
```
    $ make deploy-stand-front-b2b s=elisei1 v=10.205.0
```

### Релиз

1. Собрать релиз с версией `12.0.27` и задеплоить образ в тестинг:
* для интранета ([ссылка на стейдж](https://deploy.yandex-team.ru/stage/wiki-back-intranet-testing)):
```
    $ make release-wiki v=12.0.27
```
* для B2B ([ссылка на стейдж](https://deploy.yandex-team.ru/stage/wiki-back-b2b-testing)):
```
    $ make release-b2b v=12.0.27
```

2. Задеплоить релизный образ в продакшен:
* для интранета ([ссылка на стейдж](https://deploy.yandex-team.ru/stage/wiki-back-intranet-production)):
```
    $ make deploy-prod-wiki v=12.0.27
```
* для B2B ([ссылка на стейдж](https://deploy.yandex-team.ru/stage/wiki-back-b2b-production)):
```
    $ make deploy-prod-b2b v=12.0.27
```

