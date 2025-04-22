# Header

## Как добавить пункт меню

Добавить в файле `./const.ts` в `menuItems` объект со следующими свойствами:

- `id` (`string`) - ID для пункта меню. Он будет использован для получения перевода из i18n. Ключ для перевода будет
  являться конкатенацией `"header-menu-item-"` + `id`
- `to` (`string | ToProp`) - ссылка куда будет вести пункт меню, если этого поля нету, то пункт меню в ссылку оборачиваться не будет.
  Также вместо строки можно передать объект со следующими свойствами:
  - `service` (`SupportedService`) - id сервиса из `@metrika/shared/domain/services`
  - `href` (`string`) - просто ссылка целиком
  - `appendFromHeader` (`boolean`) - добавляет `utm_source` к URL
- `external` (`boolean`) (optional) - если `true` то будет использоваться внешняя ссылка
- `path` (`string|string[]`) (optional) - если текущий `pathname` будет равен тому что здесь, то пункт меню будет подсвечиваться
  как активный. Если `path` отсутствует то смотрим на `to`
- `disabled` (`boolean`) (optional) - является ли пункт меню неактивным
- `content` (optional) - объект с полями:
    - `MenuItem` - React компонент. __Важно:__ ему в `children` будет передан перевод из i18n
    - `itemProps` (optional) - пропсы для `MenuItem`
