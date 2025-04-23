# realty-front-amp

[AMP версия](https://amp.dev/about/websites/)

## Основная информация

| Service | URL                                                                                                           |
|---|---------------------------------------------------------------------------------------------------------------|
| Arcanum CI | https://a.yandex-team.ru/projects/realty/ci/releases/timeline?dir=classifieds%2Frealty-frontend&id=realty-amp-www |
| Deploy | https://admin.vertis.yandex-team.ru/services/realty-front-amp                                                 |
| Grafana | https://grafana.vertis.yandex-team.ru/d/yQvo5o6iz/realty-nodejs-frontends?var-job=realty-front-amp            |

## Хосты

| Environment | URL |
|---|---|
| Testing | https://realty.test.vertis.yandex.ru/amp/ <br> https://branch-${branch}.realty.test.vertis.yandex.ru/amp/ |
| Production | https://realty.yandex.ru/amp/ |


##Особенности

- ssr-only
- нет бандлов (сервер возвращает уже готовый html)
- используется [isomorphic-style-loader](https://github.com/kriasoft/isomorphic-style-loader) для инлайнового подключения стилей в head (в webpack-utils этот лоадер подключен для файлов *.amp.css)
- подключен [amp-optimizer](https://github.com/ampproject/amp-toolbox/tree/main/packages/optimizer#amp-optimizer) для улучшения производительности
- есть [ряд ограничений](https://amp.dev/documentation/guides-and-tutorials/learn/spec/amphtml/)
- некоторые стандартные html элементы заменены [amp-компонентами](https://amp.dev/documentation/components/)
- amp-страница **обязана** пройти [валидацию](https://amp.dev/documentation/guides-and-tutorials/learn/validation-workflow/validate_amp/?format=websites) (в деве есть 1 ошибка валидации "Custom JavaScript is not allowed" из-за того, что в консоль браузера выводится INITIAL_DATA и INITIAL_STATE)
- [CORS](https://amp.dev/documentation/guides-and-tutorials/learn/amp-caches-and-cors/amp-cors-requests/)
