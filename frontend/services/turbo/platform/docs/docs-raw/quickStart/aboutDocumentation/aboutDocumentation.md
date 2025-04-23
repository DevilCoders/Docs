## О документации

### Формат документации

Документация пишется в `markdown`:
- [вики](https://ru.wikipedia.org/wiki/Markdown) [en](https://en.wikipedia.org/wiki/Markdown)
- [синтакстис](https://github.com/sandino/Markdown-Cheatsheet)

Маркдаун на самом деле семейство форматов, мы используем `github-flawored`. Это означает, что если в превью
гитхаба выглядит прилично, то прилично будет выглядеть и в документации (и наоборот). Можно проверять, например,
в [gists](https://github.yandex-team.ru/gist).

У нас есть небольшие ограничения:
- Мы используем заголовки со второго по четвертый уровень (`##`, `###`, `####`)
- У нас нет чекбоксов

### Расширение формата.

У каждого элемента меню должно быть заглавие. Заглавием считается:

```markdown
## Имя блока на русском
```

В документацию можно включить `xml`-пример блока. Для этого необходимо сделать:
```markdown

## Имя блока

`example:<название-примера.xml>`
```

### Где писать документацию

Документацию к отдельным блокам нужно писать в самих файлах блоков. В зависимости от того, где живет
блок (в платформе или «традиционных» блоках) нужно писать либо в `(touch-phone|common|desktop).blocks/<component-name>`,
либо в `platform/components/<component-name>`.

Описанием блока служит `README.md`, примеры нужно класть к
[компонентам в блоках](https://github.yandex-team.ru/serp/turbo/tree/dev/common.blocks/image/image.examples) для бэмовых компонентов
или [в папку __tests__](https://github.yandex-team.ru/serp/turbo/tree/dev/platform/components/BeruExpandableText/__tests__/examples)
для компонентов платформы.

Общую документацию нужно писать в
[`platform/docs/docs-raw/начало работы/<название>/<название>.md`](https://github.yandex-team.ru/serp/turbo/tree/dev/platform/docs/docs-raw/начало%20работы/about-documentation).

Ничего не понятно, что-то не так работает, что делать? Писать [werreour@](https://staff.yandex-team.ru/werreour) или [releu@](https://staff.yandex-team.ru/releu).
