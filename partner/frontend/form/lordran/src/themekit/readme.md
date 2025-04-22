# Инструкция по работе с темами

В библиотеке компонентов lego есть возможность создать собственную тему для кастомизации компонентов.
Для этого используется инструмент Themekit, который из yml-файлов (токенов) может собрать необходимые .css-файлы.

## Работа с Themekit
```sh
├── themekit
│   ├── build                               # собранные темы
│   │   ├── themes
│   │   │   ├── direct
│   ├── themes
│   │   ├── direct
│   │   │   ├── tokens                      # конфигурации стилей компонентов
│   │   │   │   ├─ button.tokens.yml
│   │   │   │   ├─ ...
│   │   │   │   └─ radioButton.tokens.yml
│   │   │   └── direct.theme.json           # объявление темы
│   └── themekit.config.json                # настройки сборки тем
└── ...
```

## Установка
```sh
npm i -DE @yandex/themekit
```

## Работа с конфигурацией
При помощи конструктора тем https://bem.github.io/yandex-ui-themer/old/ можно переопределить параметры компонентов и сформировать из них yml-токены для того, чтобы в последующем собрать из них .css-файлы.

## Сборка стилей
Из директории `themekit`:
```sh
npx themekit build
```

## Использование темы
```js
// src/features/Feature/Feature.js
import {cnTheme} from '@yandex-lego/components/Theme';
import {theme} from 'static/themekit/presets/customTheme';

// Переопределение всех параметров внутри конкретного компонента
const Feature = () => (
  <div className={cnTheme(theme)}>
    <Button view="default" size="m">
        Content
    </Button>
  </div>
)
```

## Полезные ссылки
* https://github.com/bem/themekit библиотека themekit 
* https://lego.yandex-team.ru/lego-components/components/theme/usage документация по использованию темы в lego
* https://bem.github.io/yandex-ui-themer/old/ конструктор тем
