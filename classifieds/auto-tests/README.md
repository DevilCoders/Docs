## Auto tests project for vertical services

Разработка ведётся по [github flow](https://guides.github.com/introduction/flow/)

[How to Write a Git Commit Message](http://chris.beams.io/posts/git-commit/)

Для сборки проекта и запуска тестов используется [apache maven](https://maven.apache.org)  
settings.xml для него можно взять [здесь](settings.xml)

Для отчётов используется [Allure](http://allure.qatools.ru)

### Локальный запуск

В auto-tests/.../resources создаем файл `testing.properties`:

```
   webdriver.local=true
   webdriver.browser.name=chrome
   aab_partner_key=...
   tus.token=...
   baseCookies=gids=213,env=testing,exp_flags=without_exp,holiday-popup=closed,hide_promo_about_comments=true,navigation_promo_seen-recalls=true,discount-popup=closed,great-deal-popup=closed,autoru-exclusive-popup=closed,online_view_banner_hidden=true
```

Здесь же можно прописать property, которые хотим переопределить.
`aab_partner_key` - это секрет [из секретницы](https://yav.yandex-team.ru/edit/secret/sec-01dp0t66zeygf580c2j76qjjsd)
Нужен для того, что бы сгенерить куку для антиадблока. [Подробнее тут](docs/anti_ad_block.md)  
`baseCookies` - тут прописан флаг для отключения всех экспериментов и всякие штуки что бы промо поп-апы не мешались
тестам

Для работы тестов, которые создают аккаунт в Яндекс.паспорте, требуется добавить параметр `tus.token` в файл `testing.properties`.
Токен генерируется для Яндекс.ID, нужно открыть [гайд по TUS](https://wiki.yandex-team.ru/tus/#autentifikacija)
и в блоке **Аутентификация** перейти по ссылке для получения OAuth токена.

### Новые моки

Добавлена возможность гибкого создания объектов моков.
- [гайд](https://github.com/YandexClassifieds/auto-tests/blob/master/new_mocks_guide.md) по применению;
- описание работы [здесь](https://github.com/YandexClassifieds/auto-tests/blob/master/new_mocks.md).

### Проверка запросов с помощью DevTools Selenium4

Теперь если надо проверить, что из браузера ушёл правильный запрос (метрика или просто запросы на сохранение), надо
использовать новый DevTools из Selenium4. Старых `*ProxyModule` и `ProxySteps` больше нет  
[Подробности в этой доке](docs/devtools.md)

### Codestyle

- Oracle Code Conventions for the Java Programming Language

- [Wiki](https://wiki.yandex-team.ru/users/vicdev/codestyleautotests)

### CI

- [TeamCity](https://t.vertis.yandex-team.ru/project/Verticals_Testing_Autoru)

### Lombok

Проект использует [lombok](https://projectlombok.org/)  
Плагин стоит в IDEA по дефолту
