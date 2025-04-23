# Другое

## contribs

* [contribs](../../contribs/README.md)
* [component-inspector](../../contribs/component-inspector/README.md)
* [images-components](../../contribs/images-components/README.md)
* [internal](../../contribs/internal/README.md)
* [perf](../../contribs/perf/blocks-common/perf/perf.md)
* [lodash](../../contribs/lodash/README.md)
* [preloader](../../contribs/preloader/README.md)
* [video-player](../../contribs/video-player/README.md)
* [video/player2](../../contribs/video-player/api/blocks-common/player2/README.md)
* [video/sandbox client](../../contribs/video-player/api/blocks-common/sandbox/README.md)
* [video/sandbox static](../../dev/contribs/video-player/sandbox/blocks-sandbox/README.md)

## Устарело / Редко используется
* [Сборки fiji на trendbox-ci](https://github.yandex-team.ru/mm-interfaces/fiji/blob/dev/.trendbox-ci/README.md)


Если задача обновить `node_modules` до свежей версии, надо сделать `git pull --rebase && make update`.

### SPOK

* Что делать, если блок пойдёт в спок
  * добавить spok: yes в deps блока
  * добавить `_spok_yes` к кийсету
  * как обычно, сделать `fiji tanker`
* Что делать, если блок не пойдёт в спок
  * добавить в чёрный список (в sakhalin, images или video)
    * Для этого найти функцию `getBlacklist` в соответствующем `spok.priv.js`
      * [sakhalin](../../sakhalin/blocks-common/spok/spok.priv.js)
      * [images](../../images/blocks-common/spok/spok.priv.js)
      * [video](../../video/blocks-common/spok/spok.priv.js)

### Underhood: Сборка с инклюдами

> См. подкапотные особенности сборки в [Сборка инклюдами](./include.md)
