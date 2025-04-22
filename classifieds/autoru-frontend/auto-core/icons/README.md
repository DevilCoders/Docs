Здесь лежат иконки в формате `svg` с размером по умолчанию 24x24 (`viewBox="0 0 24 24"`).

**Наименование:**

- если применена выворотка, то добавляется суффикс `-filled`: `alert-filled`;
- если иконка вписана в окружность — суффикс `in-circle`: `question-in-circle`;
- если размер иконки по умолчанию другой — добавляется размер: `favorites-16.svg`, `avatar-48.svg`.

Суффиксы могут комбинироваться: `profile-filled-36.svg`, `alert-filled-in-circle-48.svg`.

Разрешённые размеры: 12, 16, 24, 36, 40, 48, 64, 128. (см. https://a.yandex-team.ru/arcadia/classifieds/autoru-frontend/auto-core/react/components/islands/IconSvg/IconSvg.js#L18)

Иконки, которые не соответствуют этим правилам, специально править не стоит, но, если вы затрагиваете их в своём таске, нужно привести к вышеописанным гайдам.

**Источник правды — Figma**, все иконки должны быть на этой странице: https://www.figma.com/file/bwnGVVeVHFnB5WZ0t0OvIHM8/Auto-%E2%80%A2-Icons?node-id=4%3A65

**Storybook**: http://autoru-front-storybook-web.vrts-slb.test.vertis.yandex.net/?path=/story/icons--svg-sprite
