## Автотесты на сервис Яндекс.Недвижимость

Разработка ведётся по [github flow](https://guides.github.com/introduction/flow/)

[How to Write a Git Commit Message](http://chris.beams.io/posts/git-commit/)

Для сборки/деплоя проекта используется [apache maven](https://maven.apache.org).
Settings.xml для него можно взять [здесь](https://github.yandex-team.ru/qatools/settings.xml).

Для отчетов используется [Allure](http://allure.qatools.ru)
 
### Локальный запуск
В .../resources создаем файл `testing.properties`:  
```
   webdriver.local=true
   webdriver.browser.name=chrome
   realty.production.uri=https://realty.orion-01-sas.dev.vertis.yandex.ru
   realty.testing.uri=https://realty.test.vertis.yandex.ru
   realty.mobile.uri=https://m.realty.test.vertis.yandex.ru
   passport.testing.url=https://passport-test.yandex.ru/
   webdriver.browser.version=56.0
```
Здесь же можно прописать property, которые хотим переопределить.

Для macOs необходимо отключить AirDrop:
```sudo ifconfig awdl0 down```
```networksetup -setv6automatic Wi-Fi```

### Codestyle
- Oracle Code Conventions for the Java Programming Language

### CI
- [TeamCity](https://teamcity.yandex-team.ru/project.html?projectId=Verticals_Testing_Realty&tab=projectOverview)

### Lombok
Проект использует [lombok](https://projectlombok.org/)
Необходим плагин для IDE.

### AdBlock extension
Для того, чтобы запустить тесты на браузере с расширение AdBlock Plus (пока только для chrome)
Нужно добавить в `testing.properties`:
 `extension.adblock.enable=true`
 
 Загрузить расширения можно [тут](https://downloads.adblockplus.org/devbuilds/adblockpluschrome/)