# maps-tanker

NPM-модуль скачивания переводов из танкера и сборки шаблонов.

## Установка

```
npm install @yandex-int/maps-tanker --registry http://npm.yandex-team.ru --save-dev
```

## Использование

### Выгрузка и компиляция

```ts
import * as tanker from '@yandex-int/maps-tanker';

async function runTanker() {
    const {asts} = await tanker.buildAsts(
        // Языки, для которых необходимо выполнить сборку.
        ['ru', 'uk'],
        {
            // Базовый урл для API танкера
            baseUrl: 'https://tanker-api.yandex-team.ru',
            // Название проекта - единственное обязательное поле.
            project: 'projectName',
            // Ветка проекта, по умолчанию master.
            branch: 'master',
            // Токен указывать необязательно.
            token: 'OAuth token',
            // Параметр включает выгрузку ключей на языке по умолчанию вместо пустых переводов.
            safe: false,
            // Параметр, который нужно передавать, если нужны неподтвержденные переводы.
            includeUnapproved: true,
            // Нужно ли заменять небезопасные html-сущности на unicode-символы (&mdash; -> —).
            replaceHtmlEntities: true
        }
    );
    const compileOptions = {
        // Имя alias'а, в котором будут описаны типы словаря.
        identifierName: 'I18nKeysets',
        // При наличии этого свойства - происходит транспиляция в js с учетом указанных опций.
        compilerOptions: {
            target: 'es5'
        }
    }
    // В compiledFiles - объект, где ключами являются языки, а значениями - string'и с содержимым typescript (при наличии compilerOptions - javascript) файла.
    const {compiledFiles} = mapsTanker.compileFiles(asts, compileOptions);
    // В compiledFile - string с содержимым typescript (при наличии compilerOptions - javascript) файла типов.
    const {compiledFile: typesFile} = mapsTanker.compileTypesFiles(asts.ru, compileOptions);
}
```

### Выгрузка, подготовка и генерация типов

```ts
const tanker = require('@yandex-int/maps-tanker/server');

tanker.downloadAndPrepare({
    buildPath: '<some_path>',
    languages: ['ru', 'en'],
    buildOptions: {
        project: '<project_name>',
        branch: 'master',
    }
});
```

### Использование на сервере

```ts
// Класс для работы с загруженными переводами.
// Подходит для работы на сервере, так как подгруженны все переводы в память.
import {StaticI18N} from '@yandex-int/maps-tanker';
// Сгенерированные типы выгруженных переводов.
import {Language, I18nData} from './types';
// Выгруженные переводы.
import * as ruIndex from './ru';
import * as enIndex from './en';

// Инстанс класса для работы с переводами.
const projectI18n = new StaticI18N<Language, I18nData>({
    i18nData: {
        ru: ruIndex.default,
        en: enIndex.default
    }
});

// Метод для работы с переводами только русского языка.
const ruI18n = projectI18n.getSingleLangI18n('ru');

// Получение перевода только для русского языка.
const rejectReleasePhotoFail = ruI18n('notifications', 'reject-release-photo-fail', {id: ''});

// Получение перевода через общий метод.
const rejectReleasePhotoFail = projectI18n.i18n('ru', 'notifications', 'reject-release-photo-fail', {id: ''});

export {projectI18n};
```

### Использование на клиенте
```tsx
// i18n.tsx
// Класс для работы с динамически загружаемыми переводами. Подходит для работы на клиенте.
import {LoadableI18N} from '@yandex-int/maps-tanker/client';
// Сгенерированные типы выгруженных переводов.
import {Language, I18nData} from './types';

// Инстанс класса для работы с переводами.
const projectI18n = new LoadableI18N<Language, I18nData>({
    // Webpack Magic Сomment вместе с import подтянет необходимый чанк с переводом.
    importLang: (lang) => import(/* webpackChunkName: "i18n" */ `./langs/${lang}.ts`).then((module) => module.default)
});

// Можно использовать язык из контекста, без использования withI18nContext
const contextI18n = getContextI18n<Language, I18nData>();

export {projectI18n, contextI18n};

// app.tsx
import * as React from 'react';
import {I18nProvider} from '@yandex-int/maps-tanker/client';
// Инстанс класса для работы с переводами.
import {projectI18n, contextI18n} from 'i18n';
// Сгенерированные типы выгруженных переводов.
import {Language} from 'types';
import Header from 'header';

const DEFAULT_LANG: Language = 'ru';

interface State {
    loaded: boolean;
}

class App extends React.Component<{}, State> {
    state: State = {
        loaded: false
    };

    componentDidMount() {
        projectI18n.registerLang(DEFAULT_LANG)
            .then(() => this.setState({loaded: true}))
            .catch(() => {});
    }

    render(): React.ReactNode {
        return this.state.loaded ?
            (
                <I18nProvider<Language, I18nData> i18n={projectI18n} initialLang={DEFAULT_LANG}>
                    <span>{contextI18n('common', 'title')}</span>
                    <Header />
                </I18nProvider>
            ) :
            <span>Loading...</span>;
    }
}

export default App;

// header.tsx

import * as React from 'react';
import {withI18nContext} from '@yandex-int/maps-tanker/client';
// Сгенерированные типы выгруженных переводов.
import {I18nData, Language} from 'types';

type Props = I18nContextType<Language, I18nData>;

class Header extends React.Component<Props> {
    render(): React.ReactNode {
        const props = this.props;
        return (
            <>
                {props.i18n('header', 'title')}
                <button onClick={() => props.setLang(props.lang === 'ru' ? 'en' : 'ru')}>
                    {props.i18n('header', 'change-lang')}
                </button>
            </>
        );
    }
}

export default withI18nContext<I18nContextType<Language, I18nData>, Props>(Header);
```

### Использование плагина для Webpack

```ts
import * as webpack from 'webpack';
import {I18nPlugin} from '@yandex-int/maps-tanker/out/src/environments/server';

const langs = ['ru', 'en'];

const webpackConfigs: webpack.Configuration[] = langs.map((lang: string): webpack.Configuration => ({
    ...
    plugins: [
        new I18nPlugin({keysets, lang}),
        ...
    ]
}));

export default webpackConfigs;
```