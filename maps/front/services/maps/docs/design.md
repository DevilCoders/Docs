# Дизайн проекта

Весь дизайн распологается в Figma.

## Доступ

Писать [@glmrvn](https://staff.yandex-team.ru/glmrvn).

## Иконки

У нас используется два типа иконок:

-   сервисные: [Dev Core](https://www.figma.com/file/jot7Z2GDRtGCPQiftZJYCz/)
-   рубричные: [Dev POI](https://www.figma.com/file/bEtF3T02F6uxF9J68PuQkA/)

Все они выгружаются к нам в репозиторий специальным скриптом (см. `./tools/figma`).

### Core

-   Для подключения в JS используйте [`Icon`](../src/common/views/icon/icon.tsx).
-   Для инлайн подключения в JS используйте путь c `.raw` в имени файла `static/core/full-name.raw.svg`.

    Пример: `import zoomOut40Icon from 'static/core/zoom-out-40.raw.svg';`

-   Если вам необходимо получить ссылку на изображение в JS, то используйте [`coreIcons#getUrl`](../src/icons/core-icons.ts).
-   Для подключения в CSS используйте путь `static/core/full-name.svg`.

    Пример: `background-image: url('static/core/directions-round-48.svg');`

-   Для инлайн подключения в CSS добавляйте `.raw` в имени файла.

    Пример: `background-image: url('static/core/navi-24.raw.svg');`

### dark only theme

-   Для использования стилей тёмной темы перманентно (например в различных плеерах) - необходимо навесить на компонент класс ._dark-theme-only цвета для которого определены в ui-colors.css. Все стандартные css-переменные должны будут автоматически поменяться на значения тёмной темы.
