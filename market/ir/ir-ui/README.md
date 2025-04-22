Как развернуть в идее:
1. Поставить arc и всё такое.
2. `scripts/create-project.sh`
3. `idea ~/arc-idea/ir-ui`

Как править фронтенд - см. `src/frontend/README.md`.

Как запустить локально:
1. В режиме "как оно получится в итоге": `scripts/run-local.sh`
   - поднимет на http://localhost:8080
   - можно доусовершенствовать, или использовать кусочки
   - но в любом случае это - полная пересборка 
2. Основной режим:
   - Поднять локально postgres и создать схему idm_roles. Можно использовать docker-compose и postgres-local.yml. (TODO сделать embedded-postgres для локального запуска)
   - Настроить подключение к postgres в properties.d/development/01_application-development.properties. Если использовать postgres-local.yml, то всё настроено. 
   - Нужно добавить в конфигурацию запуска в Idea следующие параметры VM:
   ```
   -Dconfigs.path=${ARCADIA_ROOT}/market/ir/ir-ui/src/main/properties.d
   -Dlog4j.configurationFile=${ARCADIA_ROOT}/market/ir/ir-ui/src/main/conf/log4j2.xml
   -Denvironment=development
   -Dspring.profiles.active=development
   ```
   - Java: запуск `IrUi` из IDEA (для меня работает если поменять `Use classpath of module` на `ir-ui`, кто разберётся - говорите)
   - Frontend (нужна локально установленная nodejs 10.* версии): `scripts/run-frontend.sh` - запустит фронтенд на http://localhost:3000, который будет смотреть на локальный же бэк http://localhost:8080 (note: сейчас просто из браузера `/api/...` запросы работать не будут - но `curl`-ом и для JS-а - норм, это магия дефолтного React-ового бэка - смотрит на заголовок, что ожидается в ответ и не проксирует.. можно пофиксить, заменив на свою прокси)

## Роли, idm и бд

В тестинге проверка ролей отключена.
Вкл/выкл производится параметром ir-ui.tvm.idm.enabled.
IDM интегрирован только с продакшен контуром. Поэтому добавление ролей происходит только в прод бд.
Тестовая бд необходима для проверки liquibase скриптов.
Если очень хочется потестить роли на тестинге, нужно:
1. Включить ir-ui.tvm.idm.enabled
2. В тестовую базу ручками добавить пользователя и роли

Креды бд с ролями прод: https://yav.yandex-team.ru/secret/sec-01g79sjpz96dxcrygzb06nzgqb/explore/versions
Креды бд с ролями тестинг: https://yav.yandex-team.ru/secret/sec-01g6ajgkqh26t8ks0z0mjy45x5/explore/versions 
