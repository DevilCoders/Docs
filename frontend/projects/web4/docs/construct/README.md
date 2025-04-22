# Конструктор

Верстка поисковых результатов может строиться на "Конструкторе", то есть состоять из конструкторских блоков.

Каждый конструкторский блок имеет свое API, которому следуют адаптеры в реализации метода `transform()`. Попробовать конструкторский блок без адаптера можно в [документации](https://serpdocs.si.yandex-team.ru/).

Уже существует большое количество конструкторских блоков. Приступая к работе над новой фичей/блоком **проверьте наличие необходимых или похожих блоков** в проекте.

Документация:

- [Рецепты и примеры](./blocks-howto.md)
- [API](./blocks-api.md)
- [Документирование](./blocks-jsdoc.md)
- [Эксперименты](../experiments/construct.md)
- Системы:
  - [supply](./supply.md)
  - [типографика](./typo.md)
  - ["грибные карточки"](../faq/mushroom-cards-format.md)
  - [баобаб](https://wiki.yandex-team.ru/search-interfaces/baobab/#razmetkacherezkonstruktor)
  - [темы](./colorized.md)
  - [сетка](./grid.md)
- Блоки:
  - [composite](./blocks/composite.md)
  - [overlay-desktop](./blocks/overlay-desktop.md)
  - [overlay](./blocks/overlay.md)
- [FAQ](./faq.md)
