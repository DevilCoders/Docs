# Настройка редактора кода.

У нас можно использовать любой редактор кода, который тебе нравится. В этом файле мы собрали информацию о настройке самых распространенных программ.

В основном, в команде используют:
- WebStorm
- VSCode
- Vim

## WebStorm

[JetBrains WebStorm](https://www.jetbrains.com/ru-ru/webstorm/) — интегрированная среда разработки на JavaScript, CSS & HTML от компании JetBrains, разработанная на основе платформы IntelliJ IDEA.

### Плюсы:
+ Удобно резолвить конфликты, блеймить, прогонять прекоммит чеки, смотреть дифф и историю коммитов
+ Поддержка всего для разработки на js (Node, Typescript, etc..)
+ Поддержка всех популярных тулзов и линтеров (stylelint, ESLint, PostCSS etc..)
+ Spell-checking на английском языке (русский устанавливается дополнительно)
+ Удобная навигация по коду: нечеткий поиск, поиск по классам
+ Возможна интеграция с Трекером с помощью плагинов

### Минусы
- Большой размер, громоздкость
- Значительное потребление ресурсов, что критически снижает время работы от батареи
- Замедление работы или полный останов при выполнении ресурсоемких операций
- Сложный интерфейс из-за избытка неиспользуемых фич

### Настройка
1. Установка приложения из Self-Service и активация лицензии (выберите автоматическую активацию в появившемся окне после установки)
2. Установка зависимостей из package.json:<br>
    Update dependencies from package.json, run npm install в правом нижнем углу программы<br>
3. Отключение индексирования node_modules (может привести к зависанию):<br>
    на папке node_modules - контекстное меню - Mark directory as - Excluded<br>
    Preferences (Settings) -> Languages & Frameworks - JavaScript - Libraries -> Снять галочки с node_modules<br>
    Если индексирование не прекращается - смело перезапускайте программу, это приведет к повторной инициализации настроек индексирования<br>
    Если не помогает - проставить Excluded на node_modules подпапках (? должно быть необязательно)<br>
4. Настройка ESLint. После установки node_modules, ESLint должен сконфигурироваться автоматически, если этого не произошло - проверьте конфигурацию ESLint:<br>
    Preferences (Settings) -> Languages & Frameworks - JavaScript - Code Quality Tools - ESLint -> Automatic ESLint Configuration<br>
    Если это не помогло, попробуйте режим Manual ESLint Configuration и выберите файл .eslintrc.js из корня репозитория (? не тестировалось)<br>
5. Установка плагина PostCSS (для работы с файлами  .css):<br>
    Preferences (Settings) -> Plugins - MarketPlace - PostCSS<br>
6. Увеличение лимита размера файла (например, для работы с JSON - файлами больше 3мб)
    Help -> Edit custom properties -> idea.max.intellisense.filesize=\<size in Kilobytes\>

### Лайфхаки
1. Установите и настройке плагин commit message checker:<br>
    Поскольку WebStorm не затирает последний commit message, не сложно допустить ошибку и сделать коммит с неправильным комментарием. Для исключения этой возможонсти, необходимо:<br>
    1.1 Установить плагин commit message checker:<br>
        Preferences (Settings) -> Plugins - MarketPlace - Commit message checker<br>
    1.2 Настройте интеграцию с issue tracker:<br>
        Preferences (Settings) -> Version Control - Issue Navigation - Add new<br>

        Issue ID (regex): "[A-Za-z]+\-\d+"
        Issue link (replacement): https://st.yandex-team.ru/$0

    Настроенный плагин не позволит отправить коммит в ветку с комментарием, содержащим другие название ветки<br>
2. Настройте плагин Трекера для IDEA - [Развернутая инструкция (дополняется)](https://clubs.at.yandex-team.ru/tools/11108)
3. Установите Grazzie для проверки правописания на русском языке. Для этого:
    3.1 Установите плагин Grazzie
        Preferences (Settings) -> Plugins - MarketPlace - Grazzie<br>
    3.2 Добавьте русский язык в список языков для провреки
        Preferences (Settings) -> Tools - Grazzie - Languages - Add - Russian
<br>
Если работаете с WebStorm первый раз, гляньте список горячих клавиш (https://resources.jetbrains.com/storage/products/webstorm/docs/WebStorm_ReferenceCard.pdf) и посмотрите видеоуроки по работе с git в IDE.

## VSCode

Да вверху все очень красиво написано про WebStorm, но мы то знаем, что ничто не сравнится с **VSCode** 💪 (vsc gang! bang, bang!)

### Супер полезные штуки

1. **GitLens — Git supercharged** (eamodio.gitlens): я не знаю как без этого можно жить; просто пушка
2. **GitHub Pull Requests and Issues** (github.vscode-pull-request-github): смотрим ПР в редакторе; особенно полезна для больших ПР, когда нужна полная картина происходящего
3. **ESLint** (dbaeumer.vscode-eslint): must have; в доке к плагину можно найти как настроить автофикс при сохранении файла

### Прочие ништячки

1. **Code Spell Checker** (streetsidesoftware.code-spell-checker): проверка орфографии, можно установить как русский так и английский словарь
2. **File Utils** (sleistner.vscode-fileutils): позволяет очень легко работать с файлами в VSCode
3. **language-stylus** (sysoev.language-stylus): для работы с .styl-файлами (они уже умирают, но что-то еще осталось)
4. **postcss-sugarss-language** (mhmadhamster.postcss-language): для работы с postCSS
5. **Toggle Quotes** (britesnow.vscode-toggle-quotes): быстро переключаемся между '', "", ``
6. **Surround** (yatki.vscode-surround): клевая штука если нужно заключить блок кода во что бы то ни было (например, if-block)
7. **Bookmarks** (alefragnani.bookmarks): ставим закладочки в коде, чтобы быстро к ним возвращаться
8. **autoru-frontend-snippets** (integrator000.autoru-frontend-snippets): набор готовых сниппетов кода от @integrator000 (читай подробности тут - editor_plugins/vscode/snippets/how-to.md)
9. **SVG Viewer** (cssho.vscode-svgviewer): просмотр svg в редакторе
10. **Todo Tree** (gruntfuggly.todo-tree): создаем тудушки; триллион возможностей по кастомизации под себя
11. **colorize** (kamikillerto.vscode-colorize): подсвечивает цвет в css этим самым цветом. Соль в том что это работает и для глобальных переменных заданных как var(--my-color). Правда иногда тормозит с отображением, но учитывая размер нашей кодовой базы это неудивительно.
12. **Docker** (ms-azuretools.vscode-docker): для работы с Dockerfile.
13. **EditorConfig for VS Code** (editorconfig.editorconfig): для форматирования файлов согласно проектному .editorconfig
14. **Typescript React code snippets** (infeng.vscode-react-typescript): очевидно - сниппеты TS + React.
15. **REST Client** (humao.rest-client): ваще бомба, для тех кто не очень любить cli; делать http-запросы теперь можно в один клик; поддерживает обычные урлы, нотацию по стандарту (не помню какому), и курлы (что тоже важно); ответ появляется прям в редакторе, где приятно работать с его телом; все запросы можно конвертить в курл например если нужно с кем-то поделиться

## Vim
Здесь должна документация про Vim
