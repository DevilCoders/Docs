# React-компоненты

Здесь собраны все компоненты Серпа, которые используются в других сервисах Яндекса.

Все компоненты реализуются на [React](https://reactjs.org).
Большинство компонентов реализуется с использованием [@bem-react](https://github.com/bem/bem-react):

- модификации компонентов реализуются через хелперы (`withBemMod` и `compose`/`composeU`) из [@bem-react/core](https://github.com/bem/bem-react/tree/master/packages/core)
- значения для атрибута `className` компонентов генерируются через хелпер `cn` из [@bem-react/classname](https://github.com/bem/bem-react/tree/master/packages/classname)
- дочерние компоненты и некоторые дополнительные настройки прокидываются в компонент через реестры из [@bem-react/di](https://github.com/bem/bem-react/tree/master/packages/di)

Многие компоненты написаны с использованием [@yandex-int/lego-components](https://a.yandex-team.ru/arc_vcs/frontend/packages/lego-components).

Документация:

- [Рецепты и примеры](./howto.md)
- [Паттерны разработки](../patterns/components/README.md)
- [FAQ](./faq.md)


## Полезные ссылки

- [Storybook – последний trunk](https://static-storybook.s3.mds.yandex.net/web4/dev/index.html)
- [Эксперименты с компонентами в Серпе](../experiments/components.md)

### Прежде чем разрабатывать компонент

Уже реализовано большое количество компонентов.
Приступая к работе **проверьте наличие необходимых или похожих компонентов** прежде чем создавать новый.Посмотреть готовые компоненты можно в [depot системе](https://depot.yandex-team.ru/components).

Важное правила при разработки компонентов собраны в [FAQ](./faq.md).

### Создание заготовки

```bash
npm run create-component MyComponent
```

#### Unit-тесты

```bash
npm run unit # запустить все тесты
npm run unit:file -- src/Component/Component.test.ts # Запустить тест для компонента
```

### Запуск storybook

```bash
npm run deps # Устанавливаем зависимости web4
npm run examples:build # Собираем
npm run examples:start # Запускаем
```
