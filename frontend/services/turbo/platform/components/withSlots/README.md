# withSlots

HOC withSlots служит для передачи компонентов из turboJSON в компонент через именованные пропсы, а не props.children (который получался из content), где компонент можно было брать только по индексу.
Используется, например, когда нужно прокинуть в карточку лайк и комментарий.

Для этого ввели slots
https://github.yandex-team.ru/serp/turbo/blob/dev/src/core/walk.tsx#L157

Пример turboJSON
https://github.yandex-team.ru/serp/turbo/blob/dev/platform/applications/mirror/functions/common.ts#L274

Обработка, чтобы не было ошибок hydration (так, кажется, придется делать везде, где используется withSlots)
https://github.yandex-team.ru/serp/turbo/blob/dev/platform/components/Card/Card.layouts/mirror.tsx#L23

В итоге в карточке появляется свойство `reaction`
https://github.yandex-team.ru/serp/turbo/blob/dev/platform/components/Card/_Basic/Card_Basic.tsx#L166
