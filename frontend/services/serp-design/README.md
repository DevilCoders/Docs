[![oko health](https://oko.yandex-team.ru/badges/repo.svg?repoName=frontend/services/serp-design&vcs=arc)](https://oko.yandex-team.ru/arc/frontend/services/serp-design)
[![oko security](https://oko.yandex-team.ru/badges/repoSecurity.svg?repoName=frontend/services/serp-design&vcs=arc)](https://oko.yandex-team.ru/arc/frontend/services/serp-design)

# serp-design

### Оглавление
  - [Установка и запуск](#установка-и-запуск)
  - [Стейджи в YDeploy](#стейджи-в-ydeploy)
  - [Добавление новых компонентов](#добавление-новых-компонентов)
  - [Генератор: создание компонента](#генератор-создание-компонента)
    - [Что делает команда?](#что-делает-команда)
  - [Архитектура](#архитектура)
    - [Конфигурационный файл](#конфигурационный-файл)
    - [Включение компонента в список](#включение-компонента-в-список)
  - [Как контрибьютить?](#как-контрибьютить?)
  - [Как выкатить релиз?](#как-выкатить-релиз)

## Переменные окружения
Конфигурация находится в файле `./config.ts`
- `PORT` - порт на котором запускается сервер. 3000 по дефолту.
- `PROJECT_NAME` - название проекта

## Установка и запуск
1. Установить зависимости монорепы фронтенда: `npm ci` в корне монорепы (`/frontend` от точки монтирования arc)
2. Установить зависимости serp-design: `npm ci` в корне проекта
4. Установить нужные переменные окружения
5. Собираем фронтенд `npm run build`
6. Запустить `npm run start`

## Команды для разработки
- `npm run buid:frontend` - собрать фронт
- `npm run build:backend` - собрать бекенд
- `npm run build` - собирает сначала фронтенд, затем бекенд
- `npm run lint:fix` - пытается поправить все ошибки eslinta

## Стейджи в YDeploy
- [Тестинг](https://deploy.yandex-team.ru/stages/serp-design-testing). Доступен по ссылке [lsbl6a2q344lg3h7.sas.yp-c.yandex.net](http://lsbl6a2q344lg3h7.sas.yp-c.yandex.net)
- [Прод](https://deploy.yandex-team.ru/stages/serp-design-prod). Доступен по ссылке [42mgoi5vijjlewoe.sas.yp-c.yandex.net](http://42mgoi5vijjlewoe.sas.yp-c.yandex.net/)

## Добавление новых компонентов
Есть доступные команды для создания компонентов с базовым интерфейсом, а также по определенному шаблону.

Команда для создания компонента:
```
npm run component:create -- --name=NameOfComponent
```
Передавая параметр *--template=NameOfExistingComponent*, можно указать на основе какого компонента сгенерировать компонент.

Команда для переименования компонента:
```
npm run component:rename -- --name=NameOfComponent --new-name=NewNameOfComponent
```

## Генератор: создание компонента
На этом этапе мы будем описывать работу генератора.

Команда для создания компонента:
```
npm run component:create -- --name=NameOfComponent --template=NameOfExistingComponent
```

### Что делает команда?
1. Создает новый тип компонента в **enum** componentType в файле *src/components/resource/resource.typing.ts*.
В качестве типа используется значение параметра который указывается в команде: *--name=NameOfComponent*. Парметр name преобразуется в стиле kebab_case c верхным регистром букв => NAME_OF_COMPONENT и используется в качестве типа, также в качестве значения используется kebab_case с нижным регистром.
```typescript
export enum componentType {
    QUERY='Query',
    PARAGRAPH='Paragraph,
    NAME_OF_COMPONENT='Name_of_component'
}    
```

2. Создает директорию для компонента по пути *src/components/resource/* с названием NameOfComponent (указывается в параметр --name).

3. Создает конфигурационный файл компонента с базовыми настройками в созданной директории: *NameOfComponent.config.ts*
```typescript
import type { IComponent } from '../resource.typing';
import { componentType } from '../resource.typing';
import { inputElement } from '../resource.typing';
import { NameOfComponent } from './View/NameOfComponent';

const config: IComponent = {
    name: 'NameOfComponent',                    // Название компонента
    type: componentType.NAME_OF_COMPONENT,      // Тип компонента
    editor: null,                               // Компонент для представления в редактор
    view: NameOfComponent,                      // Компонент для превью
    fields: [                                   // Поля ввода
        {
            name: 'field',                      // Название поле field. По такому ключу записывается значение поле
            attr: {                             // HTML атрибуты, все свойство в объекте попадают в качестве атрибутов в элемент ввода
                placeholder: 'Field placeholder'
            },
            type: inputElement.INPUT_TEXT,      // Тип поле ввода. В данном случае используется стандартный input
            size: 12                            // Занимает 12 колонок по ширине
        }
    ]
};

export default config;
```

#### 4. Создает react-компонент который указано в качестве превью в конфигруационном файле
Создает директорию с названием View для компонента. В директории View создает следующие файлы:

- **NameOfComponent.tsx** - React-компонент с базовым интерфейсом
- **NameOfComponent.scss** - Общые(Desktop&Touch) стили для компонента
- **NameOfComponent@desktop.scss** -  Стили для Desktop устройств
- **NameOfComponent@touch-phone.scss** - Стили для Touch устройств

##### NameOfComponent.tsx:
```typescript
import React from 'react';
import type { FC } from 'react';
import './NameOfComponent.scss';
import './NameOfComponent@desktop.scss';
import './NameOfComponent@touch-phone.scss';

interface INameOfComponent {
    field: string
}

export const NameOfComponent: FC<INameOfComponent> = props => {
    const { children, field } = props;
    return (
        <div className="NameOfComponent">
            <h4>{ field }</h4>
            { children || null }
        </div>
    );
};
```

##### NameOfComponent.scss:
```typescript
// Import common styles of search-design package
@import "../../../../../node_modules/@yandex-serp-design/search/consts/styles/styles@common.scss";

.NameOfComponent {

}
```

##### NameOfComponent@desktop.scss:
```typescript
// Import desktop styles of search-design package
@import "../../../../../node_modules/@yandex-serp-design/search/consts/styles/styles@desktop.scss";

.desktop .NameOfComponent {

}
```

##### NameOfComponent@touch-phone.scss:
```typescript
// Import touch-phone styles of search-design package
@import "../../../../../node_modules/@yandex-serp-design/search/consts/styles/styles@touch-phone.scss";

.touch-phone .NameOfComponent {

}
```

5. Зарегистрирует компонент в общий список
Читает файл конфиграции по пути *src/component/resource/resource.config.ts*.
Импортирует в него конфигурацию компонента: 
**import NameOfComponent from './NameOfComponent/NameOfComponent.config.ts'**

Находит объект resourceConfig и добавляет в него новое поле: **[type.NAME_OF_COMPONENT]: NameOfComponent**.

Сортирует объект по алфавиту, и заново восстанавливает файл конфигурации. 

Также слудет запомнить что в данном записе NameOfComponent - является объектом который экспортируется из конфигурационного файла компонента.

*Команда на этом заканчивает свою работу. Далее уже в список компонентов можно увидеть только что созданный компонент.*


##  Архитектура
### Конфигурационный файл
Это общее правило для всех компонентов. Конфигурация описывается одним общим интерфейсом.
```typescript
export interface IComponent {
    /**
     * Name of component
     */
    name: string,
    /**
     * Type of component (enum componentType)
     */
    type: componentType,
    /**
     * React-component for editor (provides input elements)
     */
    editor: React.ElementType,
    /**
     * React-component for presenting data in preview
     */
    view: React.ElementType,
    /**
     * Configures passing child elements as props or as child elements to view's component.
     * True: childs will be pass as props
     */
    viewChildsInside?: boolean,
    /**
     * Fields information
     */
    fields?: IComponentField[],
    /**
     * Configures the exclusion of a component from the list.
     * Used when the component will be used as a child of a specific component
     */
    exclude?: boolean,
    /**
     * A high level means that the component is only used on top of other components.
     * True: Component will be excluded from list
     */
    highlevel?: boolean,
    /**
     * IWhen a component is created, a child element is also created. 
     */
    defaultChild?: componentType,
    /**
     * Array of component types;
     * All child components of a component can only change their types to these types.
     */
    childTypes?: componentType[] | IComponent[]
}
```

#### Интерфейс описывающий поле (IComponentField)
```typescript
export interface IComponentField {
    /**
     * Field name.
     * Used as a key to retrieve data from storage.
     * It will also be used as props([name]={value}) for the View component.
     */
    name: string,
    /**
     * Type of element.
     * The type comes from a catalog of elements that are used as standard input elements.
     */
    type?: inputElement,
    /**
     * Grid columns as bootstrap.
     */
    size?: 12 | 6 | 4 | 3 | 2 | 1,
    /**
     * Attributes object. All properties of the object will be passed to the input element.
     */
    attr?: IAttr,
    defaultValue?: string,
    /**
     * True: The height of the element will be changed if the content does not interfere.
     */
    isHeightFlexible?: boolean
}
```

### Включение компонента в список
Файл для зарегистрирования компонента находится по пути *src/components/resource/resource.config.ts*.

В нем есть объект(*resourceConfig*) в котором нужно записать конфигурацию компонента в таком формате: *[TYPE_OF_COMPONENT]: ConfigObjectOfCompoent*

```typescript
import ConfigOfComponent from './NameOfComponent/NameOfComponent.config.ts'

export const resourceConfig: IResourceConfig = {
    [type.BACKGROUND]: Background,
    [type.BACK_HEADER]: BackHeader,
    [type.BADGE]: Badge,
    [type.BADGE_RATING]: BadgeRating,
    [type.BIG_IMAGE]: Image,
    [type.BLOCK]: Block,
    [type.BUTTON_PLAY]: ButtonPlay,
    [type.CARD]: Card,
    [type.CARD_FOOTER]: CardFooter,
    [type.CARD_PERSON]: CardPerson,
    [type.TYPE_OF_COMPONENT]: ConfigOfComponent
}
```

Также необходимо импортировать конфигурацию объекта

## Как контрибьютить?

Все команды аркадии очень быстро и просто описаны, чтобы сделать порог вхождения в разработку в прототипницу чуть проще. Если появились проблемы, переходите не официальную и подробную документацию по арку и смотртите ее: https://arc-vcs.yandex-team.ru

- Создаем задачу в очереди `SERPDESIGN`, прилинковываем к эпику по разработке прототипницы:   https://st.yandex-team.ru/SERPDESIGN-7385

- Создаем ветку по названию задачу и переходим на неё:
```
arc checkout -b SERPDESIGN-{номер задачи} trunk
```
Это команда создает ветку и переходит на нее.

- Делаем нужные изменения в репозитории. Добавляем файлы в staged
```
arc add .
```
- Коммитим изменения
```
arc commit -m "Название коммита"
```

- Пушим изменения
```
arc push -fu users/{username}/SERPDESIGN-{номер задачи}
```

- Создаем пулл ревест:
```
arc pr create
```
- Вставляем в название пулл ревеста номер задачи и название тикета, чтобы оно подхватилось арканумом.

Пример:
```
SERPDESIGN-777: Обновление пакетов в репозитории
```

- После того как ветка больше не нужна просто переключаемся на trunk -> `arc checkout trunk`, и дальше делаем другую задачу на новой ветке (смотри пункт 1)


## Получение свежего транка:
```
arc pull trunk
```

## Чтобы обновить ветку под свежий транк, в нужной ветке:
```
arc pull trunk
arc rebase trunk
```

## Обновление документации
Если нужно обновить только документацию, то можно не создавать задачу а использовать название ветки `TRIVIAL`. Изменять программный код в таких пулл ревестах нельзя.

# Как выкатить релиз?

Плановой выкатки релизов сейчас нет, все релизы катаются руками. Катить релиз можно [через арканум](https://a.yandex-team.ru/projects/frontend/ci/releases/timeline?dir=frontend%2Fservices%2Fserp-design&id=release&sidebarFilter=serp). Создается релизный тикет SEAREL с запуском тестов и сборки, если все проходит стейдж поедет на деплоные поды в YDeploy.
