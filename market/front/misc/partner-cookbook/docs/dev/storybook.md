# Storybook

[Официальная документация](https://storybook.js.org/)

<details>
<summary>Зачем storybook в ПИ</summary>

- для просмотра существующих общих компонентов, которые пока не попали в Левитан
- для возможности "поиграть" незнакомым компонентом без создания "песочницы" на странице ПИ
- для разработки компонентов без логруса
- дать дизайнерам возможность просматривать компоненты проекта, которые еще не мигрировали в Левитан
</details>

<details>
<summary>Почему storybook, а не другой инструмент</summary>

- возможность создавать плэйграунды на mdx, jsx, tsx
- возможность связывать документацию ссылками и быстро подключать существующие Readme.md
- возможность работать с redux-стором (через плагин). Необходимо для всех компонентов, использующих i18n
- возможность подключить фигму (через плагин) для сопоставления референсного значения с результатом разработки
- самое большое количество контрибьютеров среди систем документации компонентов
</details>

## Запуск

Некоторые компоненты могут использовать танкерные ключи и для получения переводов необходимо установить переменную окружения (лучше положить в `.env`):
```bash
TANKER_OAUTH_TOKEN=AQAD-XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX
```
Получить Oauth-токен для танкера можно [здесь](https://nda.ya.ru/3SjQY7)

Собственно запуск storybook:
```bash
npm run storybook
```

## Как написать документацию на компонент

Storybook ищет документацию в файлах:
- `~/client.next/components/**/*.stories.mdx`
- `~/client.next/components/**/*.stories.(js|jsx|ts|tsx)`

Предпочтительно использовать `*.tsx` вариант, чтобы работала система проверки типов.

###  Общая заготовка для документирования компонента
```tsx
import React from 'react';
import type {Meta} from '@storybook/react';

import {withI18nKeysets} from '../utils/stories/utils/I18n';

import FakeComponent from '.';

// Мета-информация для документации компонента
export default {
    title: 'Components/FakeComponent', // Определяет где в сайдбаре сторибука будет выведена документация на компонент
    component: FakeComponent, // В таблицу props'ов компонента подтянет типы и описание полей (если для них указан JSDoc)
    decorators: [withI18nKeysets(['pages.common'])], // Можно указать кейсет танкера, если компонент использует i18n, хотя претенденты на перемещение в левитан не должны содержать i18n
} as Meta;

type StoryArgs = {
    isOpen: boolean;
};

// Story - вариант использования компонента. Ниже определяется story с названием Primary
export const Primary = ({isOpen}: StoryArgs) => {
    return <FakeComponent isOpen={isOpen} />
}

// Аргументы story, которыми можно будет "играть" в сторибуке
Primary.args = {
    isOpen: true, 
};

// Параметры story. Здесь можно определить параметры для плагинов при отображении данной story, например:
// - ссылку на figma, по которой разрабатывался компонент
// - способ отображения кода на вкладке Docs
Primary.parameters = {
    design: {
        type: 'figma',
        url: 'https://www.figma.com/fake-url',
    },
};
```

### Вывод в Storybook'е md-документации
В md-файл можно вставить несколько stories и указать места, где их необходимо вывести

Файл с md-документацией `sampleDoc.mdx`:
```md
import { Story } from '@storybook/addon-docs';

# Заголовок для документации

## Раздел, в котором показываем Primary-story

<!-- sampleDoc.stories.mdx-->

<Story id="components-sampledoc--primary"  />

## Раздел без story

Какая-то документация
```

Файл для подключения документации в Storybook `sampleDoc.stories.tsx`
```tsx
import React from 'react';
import {Meta} from '@storybook/react';

import sampleDoc from './sampleDoc.mdx';

export default {
    title: 'Components/SampleDoc',
    parameters: {
        docs: {
            page: sampleDoc,
        },
    },
} as Meta;

export const Primary = () => <div>Можно отобразить компонент, для которого написана документация</div>
```