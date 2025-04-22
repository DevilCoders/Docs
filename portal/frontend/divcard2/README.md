# Дивная библотека на TypeScript

[Документация DivKit](https://doc.yandex-team.ru/divkit/overview/)

## Что это и зачем
Библиотека `divcard2` предоставляет типобезопасные инструменты для генерации JSON-описаний высокоуровневой верстки дивных карточек для Морды, ПП и Алисы.

## Пример

```typescript
import {
    ContainerBlock,
    TextBlock,
    Template,
    TemplateBlock,
    TemplateCard,
    Templates,
    templateHelper,
    rewriteVars
} from 'divcard2';

const templatesMap = rewriteVars({
    sampleBlock: new ContainerBlock({
        items: [new TemplateBlock('sampleHeader')],
        paddings: new Template('paddings')
    }),
    sampleHeader: new ContainerBlock({
        items: [new TextBlock({text: new Template('title')}]
    })
});

const thelper = templateHelper(templatesMap);

console.log(JSON.stringify(new TemplateCard(new Templates(templatesMap), {
    log_id: 'div2_sample_card',
    states: [
        {
            state_id: 0,
            div: thelper.sampleBlock({
                title: 'Пример',
                paddings: {left: 5}
            })
        }
    ]
})));
```

В результате `JSON.stringify(new TemplateCard(...))` вернет следующий JSON:
```json
{
  "templates": {
    "sampleBlock": {
      "type": "container",
      "items": [
        {
          "type": "sampleHeader"
        }
      ]
    },
    "sampleHeader": {
      "type": "container",
      "items": [
        {
          "type": "text",
          "$text": "title"
        }
      ]
    }
  },
  "card": {
    "log_id": "div2_sample_card",
    "states": [
      {
        "state_id": 0,
        "div": {
          "type": "sampleBlock",
          "title": "Пример",
          "paddings": {
            "left": 5
          }
        }
      }
    ]
  }
}
```

Более сложные примеры верстки карточек можно посмотреть в репозитории [geohelper](https://a.yandex-team.ru/arc_vcs/portal/geohelper/server/api/v3/divproxy/blocks/div2).

## Runtime-валидация шаблонов
В режиме разработки предусмотрена runtime-валидация создания экземпляров шаблонов. Валидация выполняется в конструкторе `TemplateCard` и для ее работы нужно включить переменную среды `NODE_ENV=development`.

## Типизированные шаблоны (compile-time валидация)
Для проверки компилятором набора шаблонных свойств можно использовать вспомогательную функцию `templateHelper`. Типизация работает корректно только при включенном флаге [strictNullChecks](https://www.typescriptlang.org/docs/handbook/compiler-options.html) в tsconfig.json!

```typescript
const block = new TemplateBlock('sampleHeader', {
    title: 'Пример'
});

// вариант с templateHelper проверяет список параметров и их типы во время компиляции
const safeBlock = thelper.sampleHeader({
    title: 'Пример'
});
```

## Гарантии валидности divjson2

При разработке карточки нужно самостоятельно следить за тем, чтобы

- Текстовые строки не были пустыми;
- Урлы картинок, действий и др. были валидными;
- Массивы не был пустыми.

В сомнительных случаях сверяйтесь с [divkit](https://doc.yandex-team.ru/divkit/overview/)

## Обновление библиотеки по JSON-схеме

Основные типы данных автоматически генерируются по схеме. Для этого к репозиторию подключены два сабмодуля:
- [mobile-homapi-binaries](https://bitbucket.browser.yandex-team.ru/projects/stardust/repos/mobile-homeapi-binaries) – бинарники генератора типов по схеме. Исходники генератора находятся в репозитории [mobile-homepi-ios](https://bitbucket.browser.yandex-team.ru/users/askvortsov/repos/mobile-homeapi-ios).
- [div-schema](https://bitbucket.browser.yandex-team.ru/projects/ML/repos/div-schema) – схемы с описанием структур данных.

Обновление библиотеки в соответствии со свежей схемой выглядит следующим образом:

```bash
# инициализация сабмодулей, если они ещё не проинициализированы
git submodule update --init

# обновление схемы
cd morda-schema
git checkout master
git pull
cd ..

# генерация кода
./generate_macos.sh
# или
./generate_linux.sh
```

Далее создаём пулл-реквест как обычно.

## Ссылки
[Документация divkit](https://doc.yandex-team.ru/divkit/overview/)

[Подключение источника и разработка дивного блока в Геохелпере](https://wiki.yandex-team.ru/Morda/div-platform/geohelper/)

[Чат поддержки в Telegram](https://t.me/joinchat/FtO3zxdxMWOsQzndJmlC0Q)
