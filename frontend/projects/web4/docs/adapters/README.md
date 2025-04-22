# Адаптеры

Адаптер — это код, преобразующий данные от бекенда в формат, который ожидают получить React-компоненты или "Конструктор".
Адаптер пишется на каждый конкретный тип ответа (рецепт, сниппет букинга, авто.ру и т.д.).

Технически есть два способа реализации адаптера:
- [TypeScript](https://www.typescriptlang.org/)-адаптер для платформы ["Табурет"](https://a.yandex-team.ru/arc_vcs/frontend/packages/taburet) с шаблонизацией через React-компоненты или Конструктор
- Priv-адаптер с шаблонизацией на Конструкторе. Устаревшая реализация, которая постепенно конвертируется в TS-форму (см. [статус конвертации](https://wiki.yandex-team.ru/search-interfaces/architecture/adapters-migration/)). **Все новые адаптеры должны быть реализованы на TypeScript**

![Схема работы](https://jing.yandex-team.ru/files/vttly/serp-adapters.png)

```bash
adapters/ — priv-адаптеры, которые нужно конвертировать
src/
 ├── features/**/*.server.tsx — TypeScript-адаптеры
```

Документация:

- [Рецепты и примеры](./howto.md) (TypeScript)
- [Эксперименты](../experiments/adapters.md)
- [Паттерны разработки](../patterns/adapters/README.md)
- Системы:
  - [Ajax](../systems/ajax.md)
  - [I18n](../systems/i18n.md)
- [Устаревшие priv-адаптеры](./deprecated-priv.md)
- [FAQ](./faq.md)
