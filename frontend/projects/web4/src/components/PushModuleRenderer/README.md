# Пуш-модуль (aka пуш-бандл)

Реализация идеи условной доставки компонент только по требованию.

Предыстория https://wiki.yandex-team.ru/serp/pushbundle/#propushbundle

Актуальный стек накладывает новые ограничения и даёт новые возможности.
Парадигма "доставлять необходимые кусочки статики" преобразуется в парадигму "доставки компонент по требованию".

## Использование
Необходимо импортировать `PushModuleRenderer` и передать в метод `pushModuleRendererImport` ровно один параметр `import(path)`, где `path` – путь к компоненту, который, возможно, не понадобится на клиенте (например, в случае зависимостей от `props`).

```js
import PushModuleRenderer from '../../../components/PushModuleRenderer';

new Registry().fill({
    conditionalComponent: PushModuleRenderer.pushModuleRendererImport(import('../components/conditionalComponent')),
});
```

Пример использования: [LearnSerpPushModule](https://a.yandex-team.ru/arc/trunk/arcadia/frontend/projects/web4/src/features/LearnSerpPushModule)

## Технические подробности
### Проблематика
На клиенте механизм доставки кода по требованию хорошо реализуют [динамические импорты webpack](https://webpack.js.org/guides/code-splitting/#dynamic-imports).
Весь код, который требуется только после пользовательского действия или какого-то события, лучше доставлять клиенту именно через них.

Но на сервере такая конструкция не работает:
 - `import()` - это асинхронная операция, а шаблоны в RR обязательно должны работать синхронно
 - серверный код собирается tsc, в котором нет механизмов из webpack

### Решение
Создать компонент, который будет уметь работать:
 - синхронно на сервере (во время шаблонизации, докладывая свой бандл в общий список бандлов рантайма)
 - синхронно на клиенте (при гидрации, если во время шаблонизации бандл отправили на клиент)
 - асинхронно на клиенте (использовать [react-loadable](https://github.com/jamiebuilds/react-loadable), если компонент не нужен был на сервере)

**Примечание**. Пуш-модуль работает описанным выше образом только в testing/production окружении. В development-окружении он фолбэчится на динамическую загрузку через react-loadable.

### ts-push-module-definition
Часть кода генерируется трансформером `ts-push-module-definition`.
[Подробнее в его документации](https://a.yandex-team.ru/arc/trunk/arcadia/frontend/packages/ts-push-module-definition/README.md).

## Известные проблемы
### [SERP-123461](https://st.yandex-team.ru/SERP-123461) (fixed)
### [SERP-96301](https://st.yandex-team.ru/SERP-96301)
