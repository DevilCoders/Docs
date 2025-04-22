# Яндекс.Репетитор

Клиентская часть образовательного сервиса

**[Production](https://yandex.ru/tutor/)**  
**[Hamster](https://rctemplates-shared.hamster.yandex.ru/tutor/)**  
**[Страничка на Wiki](https://wiki.yandex-team.ru/e7n/dev/tutor/)**  
**[ABC](https://abc.yandex-team.ru/services/younglings/)**  

### Технологии:
- React
- Redux
- TypeScript

## Переменные окружения
Управлять переменными окружения можно, добавив `.env` файл в локальную копию проекта
- `LOG_BUILD_PERF=1` – логировать данные о скорости сборки и работе каждого отдельного лоадера
- `ENABLE_METRIKA=1` - включить метрику при разработке.

## Доступные команды

Прежде всего необходимо выполнить:
```
nvm use
npm ci
```

### Разработка

Локальная разработка:
```
npm run dev
```

Для ускорения процесса разработки компонентов можно использовать [Storybook](#story_part)

Разработка с созданием туннеля для внутренней сети:
```
npm run public
```

Запуск svgo
```
npm run svg-opt
```

### Разработка со Storybook
<a name="story_part"></a>
[Официальная документация](https://storybook.js.org)

**Запуск**
```bash
npm run storybook
```

**Добавиление новой истории**

Новые истории необходимо класть рядом с компонентом, на который они пишутся.
Для того, чтобы добавить историю в storybook, необходимо проделать следующие шаги:
1. Создать новый файл с расширением `.examples.tsx`
2. Импортировать `storiesOf` из `@storybook/react`
3. Создать новый инcтанс `const example = storiesOf(<cn компонента>, module);`
4. Добавить историю `example.add(<имя истории>, () => <Любой jsx>)`
5. [Рекомендуется] Использовать `@storybook/addon-knobs` `example.addDecorator(withKnobs);`
5. [Опционально] Можно использовать компонент-помощник `StoryWrapper`

**Пример**
```ts
import { storiesOf } from '@storybook/react';
import { withKnobs, text, number } from '@storybook/addon-knobs';

const example = storiesOf(cnTopicListCard(), module);
example.addDecorator(withKnobs);

example.add('plain', () => {
    const customText = text('Имя поля', 'Значение по умолчанию');

    return (
        <StoryWrapper width={629}>
            <MyComponent>{customText}</MyComponent>
        </StoryWrapper>
    )
});
```

**Когда нужно писать историю**
1. Вы хотите разрабатывать компонент быстро и отдельно (нет необходимости собирать и запускать весь проект)
2. У вас нет (еще нет) данных для компонента из бекенда
3. Вы написали новый компонент и хотите, чтобы его использовали ваши коллеги
4. Вы написали новый компонент с массой параметров в API (в том числе и вложенных)
5. Вы исправили API компонента, который уже используют ваши коллеги
6. В любой непонятной ситуациии :)

### Сборка
Сборка серверной части (шаблонов)
```
# собрать все
npm run build

# собрать клиент
npm run build:client

# собрать сервер
npm run build:server
```


### Тестирование
#### Unit (мы используем Jest)
```
# Запуск всех тестов
npm run unit

# Точечный запуск одного или нескольких тестов
npm run unit <путь к тесту>
```

Отчёт в виде html-страницы сохраняется по адресу `__reports/report-unit`

#### Hermione
```
# Запуск всех тестов
npm run hermione

# Точечный запуск одного теста
npm run hermione <путь к тесту>

# Запуск через GUI (рекомендуемый способ)
npm run hermione:gui

# Режим отладки (локальный chrome-драйвер)
npm run hermione:debug
```

Настоятельно рекомендуется ознакомиться с [опциями запуска гермионы](https://github.yandex-team.ru/search-interfaces/infratest/blob/master/packages/archon-hermione/README.md).
Для переснятия скриншотов рекомендуется использовать опцию `--play`, чтобы избежать диффов из-за данных.

Отчёт в виде html-страницы сохраняется по адресу `__reports/report-hermione:ci`


## CGI-параметры
- `dump=json|1` - выводит все данные, пришедшие с бекенда, в "сыром" виде
- `ajax=1` - выводит сериализованные данные
