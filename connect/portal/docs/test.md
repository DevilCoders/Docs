## Интерфейсные тесты через Hermione

#### Общее
Для локального запуска тестов нужен локальный конфиг с паролем для пользователей.<br/>
Содержание этого файла можно посмотреть [здесь](https://wiki.yandex-team.ru/users/shevnv/connect/local-config/).

Как рунер тестов используется [Hermione](https://github.com/gemini-testing/hermione).<br/>
Моки ответов бекенда делаются с помощью [Clement](https://github.yandex-team.ru/search-interfaces/infratest/tree/master/packages/clement).

Тесты лежат в корне проекта в папке `hermione`.<br/>
В папке с тестом находятся папки:
- `cache` - замоканные ответы от бекендов
- `screens` - эталонные скриншоты для сравнения

### Как запускать
#### Запуск на мокахg
```bash
npm run ui-test
```

#### Запуск с обновлением замоканных данных и обновлением эталонных скриншотов
```bash
npm run ui-test-update
```

#### Автозапуск в Trendbox
На каждый коммит и пуллреквест запускаются тесты через [Trendbox](https://github.yandex-team.ru/search-interfaces/trendbox-ci).<br/>
Конфиг для запуска тестов сейчас лежит в корне проекта в файле `.trendbox.yml`.

