# Trendbox CI

Здесь находятся скрипты, запускающиеся в Trendbox CI ([Документация](https://github.yandex-team.ru/search-interfaces/trendbox-ci/)).

Push-события на ветку dev:
* [trendbox-ci](./trendbox-ci) — основной скрипт, запускает остальные.
* [close-related-prs](./scripts/close-related-prs) — Удаляет связанный PR с обновлением контрибов и удаляет ветку из форка.

События на PR:
* [update-web4-contribs](./scripts/update-web4-contribs) — Запускает экспорт контрибов и создаёт PR в web4 с обновлённой версией для тестинга.

Скрипты, запускаемые по расписанию в Sandbox'е:
* [shedule/retro.sh](./shedule/retro.sh) — создаёт страницы для ретро Картинок и Видео на wiki.

# Список шедулеров Fiji

Экспорт контрибов:
* [contribs/video-player](https://sandbox.yandex-team.ru/scheduler/8460/view) - запускается каждый день в 10:00
* [contribs/thumb-preview](https://sandbox.yandex-team.ru/scheduler/10305/view) - запускается каждый день в 10:00
* [contribs/images-components](https://sandbox.yandex-team.ru/scheduler/8461/view)- запускается каждый день в 10:00
* [contribs/pointer-gestures](https://sandbox.yandex-team.ru/scheduler/8463/view) - запускается каждый день в 10:00
* [contribs/preloader](https://sandbox.yandex-team.ru/scheduler/8464/view) - запускается каждый день в 10:00

DevExp:
* [Group Meeting Create](https://sandbox.yandex-team.ru/scheduler/8483/view) - запускается по понедельникам в 20:00
* [Group Meeting Publish](https://sandbox.yandex-team.ru/scheduler/8484/view) - запускается по воскресеньям в 22:20
* [ImportSprintIDs](https://sandbox.yandex-team.ru/scheduler/8485/view) - запускается каждый час
* [Retro](https://sandbox.yandex-team.ru/scheduler/8518/view) - запускается каждый второй понедельник в 10:00

# Полезное
* [Обновление images-components используя dobby](https://wiki.yandex-team.ru/search-interfaces/multimedia/images/Obnovlenie-images-components-cherez-dobby/)