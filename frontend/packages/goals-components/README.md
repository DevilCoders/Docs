# @yandex-int/goals-components

[![OKO health](https://oko.yandex-team.ru/badges/repo.svg?vcs=arc&repoName=frontend/packages/goals-components)](https://oko.yandex-team.ru/repo/search-interfaces/frontend?repoFilter=packages/forms-components)
![npm version](https://badger.yandex-team.ru/npm/@yandex-int/goals-components/version.svg)
![npm owners](https://badger.yandex-team.ru/npm/@yandex-int/goals-components/owner.svg)

Общие компоненты конструктора форм.

- [Состав пакета и roadmap](#состав-пакета-и-roadmap)
- [Установка пакета](#установка-пакета)
- [Использование в сервисе](#использование-в-сервисе)
- [Обратная связь](#обратная-связь)
- [Разработка](#разработка)
  - [Подготовка](#подготовка)
  - [Запуск](#запуск)
  - [Формат коммит-сообщений](#формат-коммит-сообщений)
    - [Соотношение type и semver-версии, которая будет выпущена в npm](#соотношение-type-и-semver-версии-которая-будет-выпущена-в-npm)
  - [API компонента](#api-компонента)
  - [Структура компонента](#структура-компонента)
    - [Версии под платформы](#версии-под-платформы)
    - [Написание тестов](#написание-тестов)
    - [Документирование](#документирование)
  - [Запуск тестов](#запуск-тестов)
    - [Если тесты не запускаются из-за проблем с тунеллером](#если-тесты-не-запускаются-из-за-проблем-с-тунеллером)
    - [Если туннель открывается / закрываeтся, но не запускает тесты](#если-туннель-открывается--закрываeтся-но-не-запускает-тесты)
    - [Если появляется ошибка ssh](#если-появляется-ошибка-ssh)
  - [Оформление PR](#оформление-pr)
  - [Выпуск релиза](#выпуск-релиза)

## Состав пакета и roadmap

Документацию и примеры использования компонентов можно посмотреть в [сторибуке Лего](https://lego.yandex-team.ru/components/goals/latest/) в разделе _GOALS/COMPONENTS_.

## Установка пакета

```bash
#⠀Пакет с компонентами
npm i @yandex-int/goals-components --registry http://npm.yandex-team.ru

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
  withViewDefault,
  Button as ButtonBase,
} from '@yandex-lego/components/Button/desktop';
import { withStateApprove, withStateReject } from '@yandex-int/goals-components/Button';

const CustomButton = compose(
  withViewDefault,
  composeU(withStateApprove, withStateReject),
  composeU(withSizeM, withSizeS, withSizeL),
)(ButtonBase);
```

В некоторых компонентах используются лего-компоненты. Для их стилизации рекомендуется подключить тему в цветах сервиса. [Подробнее про темы](https://github.yandex-team.ru/search-interfaces/frontend/blob/master/packages/lego-components/src/components/Theme/Theme.md).

```typescript
import { configureRootTheme } from '@yandex-lego/components/Theme';
import { theme } from '@yandex-lego/components/Theme/presets/default';

// Без указания root, по умолчанию body
configureRootTheme({ theme });
```

Для удобной локальной разработки выполните

- `npm link` в директории _packages/goals-components_
- `npm link @yandex-int/goals-components` в директории сервиса.

В _node_modules_ появится символическая ссылка на пакет, и можно будет разрабатываться в монорепозитории и смотреть за результатом работы в сервисе.

## Обратная связь

Если у вас возникли вопросы или предложения по пакету, напишите нам:

goals@yandex-team.ru

## Разработка

Прочтите [гайд от Лего](https://github.yandex-team.ru/search-interfaces/frontend/blob/master/projects/lego/guidelines/contribs.md).

### Подготовка

> Известно, что `git` `v2.27.0` некорректно работает со `sparse-checkout`, и последняя рабочая версия `v2.26.2`.
> Установить её через brew можно, например, так:
> ```sh
> brew extract git qfox/git --version=2.26.2
> brew install git@2.26.2 -s
> brew unlink git
> brew link git@2.26.2
> ```

1. Установите последние доступные версии [git](https://git-scm.com) и [git-lfs](https://git-lfs.github.com)
```bash
# Вариант установки git и git-lfs используя brew
brew install git git-lfs
```

2. Сделайте форк [монорепозитория](https://github.yandex-team.ru/search-interfaces/frontend)

3. Клонируйте монорепозиторий и настройте remote **upstream** на свой форк

```bash
git clone --depth 1 --single-branch -n -- git://github.yandex-team.ru/search-interfaces/frontend.git frontend
cd frontend
git remote set-url --push origin /dev/null
git remote add upstream git://github.yandex-team.ru/tools/frontend-fork.git # ссылка на ваш форк
```

4. Создайте worktree для работы с пакетами goals

```bash
git worktree add ../goals --no-checkout
cd ../goals
git sparse-checkout init --cone
git sparse-checkout set packages/lego-components packages/tools-components packages/goals-components
```

5. Отведите ветку

```bash
git fetch origin/master
git checkout -b <название ветки> origin/master
```

6. Установите зависимости

```bash
#⠀Если нужно, переключите версию ноды
nvm use 12.14.1

#⠀Установите зависимости
#⠀Понадобится версия npm >= 6.2.0
npm ci
npx --no-install lerna bootstrap --ci
```

### Запуск

```bash
npm start
```

По адресу http://localhost:8100 станет доступен сторибук.

### Формат коммит-сообщений

В монорепозитории используются [conventional commits](https://www.conventionalcommits.org/en/v1.0.0/).
Описывайте коммиты следующим образом:

`type(scope): subject`, где

- **type**: тип изменений
- **scope**: контекст изменений
- **subject**: суть изменений

Например, так:

`feat: Добавлен компонент Button`

При релизе из этих сообщений автоматически сформируется changelog.

Про scope. По стандартку это контекст изменений, который характеризует фрагмент и изменения кода. Стандарт не регламентирует четкий список т.н. скоупов и их применение. В монорепозитории в scope часто попадает имя пакета и даже нескольких, хотя это, по сути, бессмысленное дублирование информации. По сути, это тэги, список который еще предстоит выработать. Примеры: analytics, infra, abt, i18n и т.д.

#### Соотношение type и semver-версии, которая будет выпущена в npm

| type         | Для каких изменений                                                    | Версия |
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
fix(themekit): Изменено API компонента Button

BREAKING CHANGE: Модификаторы view и size нормализованы по lego-components@3
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
└── _view — Модификатор
    ├── Block_view_default.css
    └── Block_view_raised.tsx
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
cat(null, ['mixin']); // Cat mixin
cat('Tail'); // Cat-Tail
cat('Tail', { length: 'small' }, ['mixin']); // Cat-Tail Cat-Tail_length_small mixin
```

#### Версии под платформы

Компонент разделяется на версии под различные платформы с помощью [@bem-react/di](https://github.com/bem/bem-react/tree/master/packages/di).
Все уровни переопределения находятся в одной директории и разделяются, за исключением common уровня, через знак _@_.

Пример файловой структуры:

```text
src/components/Block
├── Block.registry
│   ├── desktop.ts
│   ├── mobile.ts
│   └── index.ts
├── Block.tsx — Common-реализация
├── Block@desktop.css - Desktop-стили, например, состояния наведения и фокуса
├── Block@desktop.tsx - Desktop-реализация
└── Block@mobile.tsx
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
│   └── Block.hermione.js — Hermione тесты
└── Block.spec.tsx — Unit тесты
```

Для скриншотных тестов используйте имя блока с префиксом \_goals-components\_\_:

```text
describe('goals-components_Block', () => {
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

storiesOf('Goals/Components|Block', module)
  .addDecorator(createScopeDecorator('desktop', 'goals'))
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
      <div className="Hermione">
        /* пример применения компонента  */
      </div>
    );
  });
```

### Запуск тестов

> Для запуска скриншотных тестов понадобится Git LFS.

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

Чтобы влить ветку,

- дайте доступ на запись в репозиторий роботам `robot-merge-queue` и `robot-serp-bot` в секции **Collaborators**
- отправьте команду `/merge`.

Чтобы остановить слияние веток, отправьте команду `/stop_merge`.

### Выпуск релиза

После того, как PR будет влит, запустится задача, которая выпустит новую версию и сформирует changelog из коммит-сообщений.
