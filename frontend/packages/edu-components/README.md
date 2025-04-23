# @yandex-int/edu-components 🎓

[![code style: prettier](https://img.shields.io/badge/code_style-prettier-ff69b4.svg)](https://github.com/prettier/prettier)
[![OKO health](https://oko.yandex-team.ru/badges/repo.svg?vcs=arc&repoName=frontend/packages/edu-components)](https://oko.yandex-team.ru/repo/search-interfaces/frontend?repoFilter=packages/edu-components)
![npm version](https://badger.yandex-team.ru/npm/@yandex-int/edu-components/version.svg)
![npm owners](https://badger.yandex-team.ru/npm/@yandex-int/edu-components/owner.svg)

Общие компоненты образовательных сервисов.

- [Состав пакета и roadmap](#Состав-пакета-и-roadmap)
- [Установка пакета](#Установка-пакета)
- [Использование в сервисе](#Использование-в-сервисе)
- [Обратная связь](#Обратная-связь)
- [Разработка](#Разработка)
  - [Подготовка](#Подготовка)
  - [Запуск](#Запуск)
  - [Формат коммит-сообщений](#Формат-коммит-сообщений)
  - [API компонента](#API-компонента)
  - [Структура компонента](#Структура-компонента)
    - [Версии под платформы](#Версии-под-платформы)
    - [Написание тестов](#Написание-тестов)
    - [Документирование](#Документирование)
  - [Запуск тестов](#Запуск-тестов)
  - [Оформление PR](#Оформление-PR)
  - [Выпуск релиза](#Выпуск-релиза)

## Состав пакета и roadmap

Документацию и примеры использования компонентов можно посмотреть в [сторибуке Лего](https://lego.yandex-team.ru/components/) в разделе _EDU/COMPONENTS_.

## Установка пакета

```bash
#⠀Пакет с компонентами
npm i @yandex-int/edu-components --registry http://npm.yandex-team.ru

#⠀Peer зависимости
npm i @yandex-lego/components --registry http://npm.yandex-team.ru
npm i @bem-react/core @bem-react/di @bem-react/classname
```

## Использование в сервисе

Компоненты поставляются как набор деталей. Сборка конечного результата с нужной конфигурацией осуществляется на стороне сервиса.

Например, так можно расширить кнопку из Лего темами из пакета:

```typescript
import { compose, composeU } from '@bem-react/core';
import {
  withSizeL,
  withSizeM,
  withSizeS,
  withThemeAction,
  withThemeClear,
  withThemePseudo,
  withViewDefault,
  Button as ButtonBase,
} from '@yandex-lego/components/Button/desktop';
import { withThemeApprove, withThemeReject } from '@yandex-int/edu-components/Button';

const CustomButton = compose(
  withViewDefault,
  composeU(withThemeApprove, withThemeReject, withThemeAction, withThemeClear, withThemePseudo),
  composeU(withSizeM, withSizeS, withSizeL),
)(ButtonBase);
```

В некоторых компонентах используются лего-компоненты. Для их стилизации рекомендуется подключить тему в цветах сервиса. [Подробнее про темы](https://lego.yandex-team.ru/lego-components/components/theme/usage).

```typescript
import { configureRootTheme } from '@yandex-lego/components/Theme';
import { theme } from '@yandex-lego/components/Theme/presets/default';

// Без указания root, по умолчанию body
configureRootTheme({ theme });
```

Для удобной локальной разработки выполните

- `npm link` в директории _packages/edu-components_
- `npm link @yandex-int/edu-components` в директории сервиса.

В _node_modules_ появится символическая ссылка на пакет, и можно будет разрабатываться в монорепозитории и смотреть за результатом работы в сервисе.
При линковке бывает, что пакет резолвится с разными путями внутри целевого проекта и внутри edu-components. Лечится явным указанием пути в конфиге вебпака:
```typescript
resolve: {
  alias: {
    react: path.resolve('./node_modules/react'),
    '@bem-react/di': path.resolve('./node_modules/@bem-react/di')
  }
}
```

## Обратная связь

Если у вас возникли вопросы или предложения по пакету, напишите нам:

educ@yandex-team.ru

## Разработка

Прочтите [гайд от Лего](https://a.yandex-team.ru/arc_vcs/frontend/projects/lego/guidelines/contribs.md).

### Подготовка

1. Для разработки используется система контроля версий [arc](https://docs.yandex-team.ru/devtools/intro/quick-start-guide)
2. После настройки arc и монтирования arcadia, нужно установить зависимости монорепозитория фронтенда и edu-components

```bash
cd ~/arcadia/frontend

#⠀Если нужно, переключите версию ноды (в корне лежит .nvmrc с нужной версией)
nvm use

#⠀Установите зависимости
#⠀Понадобится версия npm >= 6.2.0
npm ci
cd packages/edu-components && npm ci
```

### Запуск

```bash
npm start
```

По адресу http://localhost:8100 станет доступен сторибук.

### Формат коммит-сообщений

В монорепозитории используются [conventional commits](https://www.conventionalcommits.org/en/v1.0.0-beta.3/).
Описывайте коммиты следующим образом:

`type(scope): subject`, где

- **type**: тип изменений
- **scope**: edu-components
- **subject**: суть изменений

Например, так:

`feat(edu-components): Добавлен компонент Button`

При релизе из этих сообщений автоматически сформируется changelog.

#### Соотношение type и semver-версии, которая будет выпущена в npm

| type(scope)  | Для каких изменений                                                    | Версия |
| ------------ | ---------------------------------------------------------------------- | ------ |
| **build**    | Изменение сборки или внешних зависимостей                              |        |
| **chore**    | Выпуск новой версии, какая-то небольшая рутинная работа                |        |
| **ci**       | Изменения, связанные с CI                                              |        |
| **docs**     | Работа с документацией                                                 |        |
| **feat**     | Новая функциональность                                                 | MINOR  |
| **fix**      | Исправление багов                                                      | PATCH  |
| **perf**     | Улучшение производительности                                           | MINOR  |
| **refactor** | Рефакторинг кода                                                       | PATCH  |
| **revert**   | Откат предыдущих изменений                                             | PATCH  |
| **style**    | Изменения, которые не влияют на код (правки отступов, опечаток и т.д.) |        |
| **test**     | Работа с тестами                                                       |        |

Чтобы выпустить MAJOR, добавьте в тело коммита _BREAKING CHANGE_ и опишите изменение.

Например, так:

```text
feat(edu-components): Изменено API компонента Button

BREAKING CHANGE: <...>
```

### API компонента

Интерфейс каждого компонента должен содержать `className` и `innerRef`.

### Структура компонента

Для нового компонента создайте директорию c его именем в _src/components_.
Разбивайте код компонента на файлы согласно стилю именования [react-naming](https://ru.bem.info/methodology/naming-convention/#стиль-react):

```text
src/components/Block
├── Block.css
├── Block.tsx
├── Header — Элемент
│   ├── Block-Header.css
│   └── Block-Header.tsx
└── _theme — Модификатор
    ├── Block_theme_night.css
    └── Block_theme_night.tsx
```

В файле _Block.tsx_ задайте пространство имён:

```typescript
import { cn } from '@bem-react/classname';

export const cnBlock = cn('Block');
```

Теперь можно строить имена CSS-классов по БЭМ и использовать результат вызова `cnBlock()` в качестве идентификатора.

Пример из документации пакета [@bem-react/cn](https://github.com/bem/bem-react/blob/master/packages/classname):

```typescript
const cat = cn('Cat');

cat(); // Cat
cat({ size: 'm' }); // Cat Cat_size_m
cat('Tail'); // Cat-Tail
cat('Tail', { length: 'small' }); // Cat-Tail Cat-Tail_length_small
```

#### Версии под платформы

Компонент разделяется на версии под различные платформы с помощью [@bem-react/di](https://github.com/bem/bem-react/tree/master/packages/di).
Все уровни переопределения находятся в одной директории и разделяются, за исключением common уровня, через знак _@_.

Пример файловой структуры:

```text
src/components/Block
├── Block.registry
│   ├── desktop.ts
│   ├── touch-pad.ts
│   ├── touch-phone.ts
│   └── index.ts
├── Block.tsx — Common-реализация
├── Block@desktop.css - Desktop-стили, например, состояния наведения и фокуса
├── Block@desktop.tsx - Desktop-реализация
├── Block@touch-pad.tsx
└── Block@touch-phone.tsx
```

В файлах внутри _Block.registry_ создавайте реестры под каждый уровень переопределения и регистрируйте в них необходимые платформе версии элементов блока.

Пример содержимого _desktop.ts_:

```typescript
import { Registry } from '@bem-react/di';

import { BlockHeader } from '../Header/Block-Header';
import { BlockFooter } from '../Footer/Block-Footer@desktop';
import { cnBlock } from '../Block';

export const blockRegistry = new Registry({ id: cnBlock() });

blockRegistry.set('Header', BlockHeader).set('Footer', BlockFooter);
```

Опишите форматы реестров в _index.ts_. В большинстве случаев реестры будут иметь одинаковую структуру.

```typescript
import { BlockElement } from '../Element/Block-Element';

export interface IBlockRegistry {
  Element: typeof BlockElement;
}
```

Соберите нужную версию блока под каждую платформу.

Пример для _Block@desktop.tsx_:

```typescript
import { compose } from '@bem-react/core';
import { withRegistry } from '@bem-react/di';

import { withSomething } from '../../hocs/withSomething/withSomething@desktop';

import { Block as BlockCommon } from './Block';
import { blockRegistry } from './Block.registry/desktop';
import './Block@desktop.css';

export * from './Block';
export const Block = compose(
  withRegistry(blockRegistry),
  withSomething, // desktop specific HOC
)(BlockCommon);
```

Теперь можно получать зависимости из текущего реестра.

Пример для _Block.tsx_:

```typescript jsx
import { useComponentRegistry } from '@bem-react/di';

import { IBlockRegistry } from './Block.registry';

export const Block = () => {
  const { Header, Footer } = useComponentRegistry<IBlockRegistry>(cnBlock());

  return (
    <>
      <Header />
      <Footer />
    </>
  );
};
```

#### Написание тестов

```text
src/components/Block
├── Block.tests
│   └── Gemini.hermione.js — Hermione тесты
└── Block.spec.tsx — Unit тесты
```

Для скриншотных тестов используйте имя блока с префиксом \_edu-components\_\_:

```text
describe('edu-components_Block', () => {
  # Код тестов
});
```

#### Документирование

```text
src/components/Block
├── Block.examples.tsx
└── Block.md
```

В _Block.md_

- опишите область применения компонента
- приведите пример использования
- задокументируйте его API и возможные модификаторы
- оставьте ссылку на код компонента на github.

Описание области применения и API компонента можно сгенерировать с помощью утилиты [ts-docgen](https://github.yandex-team.ru/search-interfaces/frontend/tree/master/projects/lego/packages/ts-docgen) командой
`npx ts-docgen generate --src=src/components --components=Block`

В _Block.examples.tsx_ импортируйте содержимое _Block.md_ и создайте стори с вариантами применения компонента.
Используйте аддон [withKnobs](https://github.com/storybooks/storybook/tree/next/addons/knobs), чтобы дать пользователям возможность настроить компонент.

```typescript jsx
import React from 'react';
import { storiesOf } from '@storybook/react';
import { compose } from '@bem-react/core';
import { withKnobs, select, text } from '@storybook/addon-knobs';

const Block = /* Соберите ваш компонент */;

storiesOf('EDU/Components|Block', module)
  .addDecorator(createScopeDecorator('desktop', 'edu'))
  .addDecorator(withKnobs)
  .addParameters({
    docs: {
      readme: require('./Block.md'),
    },
  })
  .add('playground', () => {
    const theme = select(
    'theme',
    {
      red: 'red',
      green: 'green',
      blue: 'blue'
    },
    'red'
    );

    return <Block theme={theme} />;
  })
  .add('story name', () => {
    return (
      <div className="Gemini">
        /* пример применения компонента  */
      </div>
    );
  });
```

### Запуск тестов

```bash
#⠀Unit тесты
npm run unit

#⠀Отдельный unit тест
npm run unit -t SomeComponent

#⠀Сборка статики для hermione тестов
npm run hermione:build

#⠀Запуск hermione тестов с GUI
npm run hermione:gui

#⠀Отдельный hermione тест
npm run hermione:gui -- src/components/SomeComponent/SomeComponent.tests/SomeComponent.hermione.js

# Можно получить доступ к машине в гриде при помощи плагина @yandex-int/hermione-debug
# -b Запускать тесты только в этом браузере
# --grep Запускать тесты, подходящие под этот паттерн
# В самих тестах брейкпоинты ставятся через waitForEnter
npm run hermione:debug -- src/components/SomeComponent/SomeComponent.tests/SomeComponent.hermione.js -b chrome-desktop --grep "name of the test"
```

#### Если тесты не запускаются из-за проблем с тунеллером

Оставьте заявку на доступ для вашей группы. [Пример заявки](https://puncher.yandex-team.ru/tasks?id=5cc2e45ed5626d4fed44525a)

#### Если туннель открывается / закрываeтся, но не запускает тесты

Прочитайте про доступы на [wiki](https://wiki.yandex-team.ru/search-interfaces/infra/infrasre/duty/tunneler/?from=%252Fsearch-interfaces%252Finfra%252Finfratest%252Fduty%252Ftunneler%252F#vydachadostupov)

#### Если появляется ошибка ssh

[Сгенерируйте](https://github.com/evgenymarkov/mac-tutorials/blob/master/03-software/03-software.md#ssh) и добавьте ssh ключ в [стафф](https://staff.yandex-team.ru).

### CSS Переменные

Если вы обновляете дизайн-токены, то не забудьте обновить их через команду:

```bash
npm run tokens:build
```

Подробнее про [themekit](https://github.com/yarastqt/themekit)

### Оформление PR

Перед тем, как сделать PR,

- [ ] выполните `npm run build`
- [ ] напишите документацию
- [ ] снимите эталонные скриншоты для нового компонента
- [ ] убедитесь, что тесты проходят без ошибок

В заголовке PR укажите название задачи.

Если вы хотите, чтобы ваш код посмотрел конкретный разработчик, добавьте в описание `cc @username`.

После создания PR ревью не начинается автоматически.
Когда вы будете готовы отдать код на ревью, напишите в комментарии `/start`.
[Список доступных команд](https://github.yandex-team.ru/devexp/devexp#Поддерживаемые-команды)

Чтобы влить ветку, отправьте команду `/merge`.

Чтобы остановить слияние веток, отправьте команду `/stop_merge`.

Чтобы запустить сборку canary-версии пакета для тестирования в своём сервисе, отправьте команду `/canary none`.

#### Тестовый стенд

При создании PR в arcadia будет автоматически собран сторибук пакета, ссылка на который добавится в описание PR-а. 

### Выпуск релиза

После того, как PR будет влит, запустится задача, которая выпустит новую версию и сформирует changelog из коммит-сообщений.
