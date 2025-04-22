# Структура типового сервиса

Файловая структура должна быть: прозрачна, однообразна (в соотв со всеми монорепами) и максимально проста (минимальный уровень вложенности).

Пример файловой структуры:
```
- service-www
    - configs
    - constants
    - client
        - components
            - SnippetName
                - `__tests__`
                - DirtyСomponentName
                - AnotherOneComponent
                  index.js
                  i18n.js
                  style.module.css
        - pages
            - pageName
              routes.js
              App.js
              index.js
    - server
      index.js
      Dockerfile
      README.md
      nodemon.json
      webpack.config.js // require('internal-core/webpack').setup({ ... })
      package.json // npm run start, dev, test + specific service deps
- internal-core
    - client
        - components
            - Page
            - Header
            - Footer
            - SomeSharedCompoent
                - __tests__
                  ...
                  ...
    - server
        - controllers
        - middlewares
        - resources // РЕСУРСЫ ТОЛЬКО ТУТ!
    - constants
    - configs
      ...
      package.json // npm test
