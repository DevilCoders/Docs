[![OKO health](https://badger.yandex-team.ru/oko/repo/data-ui/core/health.svg)](https://oko.yandex-team.ru/repo/market-java/mbo-category)

# mbo-category-frontend

Ссылки:

- https://cm.market.yandex-team.ru - прод
- https://cm-testing.market.yandex-team.ru - тестинг

Релизный пайплайн фронтенда: https://tsum.yandex-team.ru/pipe/projects/mbo/delivery-dashboard/mbo-category-frontend

Релизы катаются по зеленому транку и выкатываются релизной машиной: https://tsum.yandex-team.ru/pipe/projects/mbo/delivery-dashboard/mbo-cm-ui-frontend  
Бекенд репозиторий: https://a.yandex-team.ru/arc/trunk/arcadia/market/mbo/mbo-category

### Запуск проекта

При первом запуске приложения, в файл `/etc/hosts` (`C:\Windows\System32\Drivers\etc\hosts` - для Windows) необходимо добавить следующие записи (это необходимо сделать только один раз):

```
127.0.0.1   localhost.msup.yandex-team.ru
127.0.0.1   localhost.msup.yandex.ru
```

Через команду в **npm**:
```bash
npm run bootstrap:hosts
```

Далее устанавливаем зависимости:

```bash
npm ci
```

Запускаем приложение:

```bash
npm start
```

Если у вас nodejs >= 12, то скорее всего при запуске приложения получите ошибку:

```bash
The certificate key "mbo-category-frontend/node_modules/@yandex-int/magicdev/data/yandex-team.pem" is invalid.
error:040650B3:rsa routines:rsa_ossl_private_decrypt:missing private key
npm ERR! code ELIFECYCLE
npm ERR! errno 1
npm ERR! frontend-ts@0.1.0 start: `react-scripts start`
npm ERR! Exit status 1
npm ERR!
npm ERR! Failed at the frontend-ts@0.1.0 start script.
npm ERR! This is probably not a problem with npm. There is likely additional logging output above.

npm ERR! A complete log of this run can be found in:
npm ERR!     "$HOME/.npm/_logs/2020-08-10T08_21_11_884Z-debug.log"
```

Для решения этой проблемы необходимо разделить сертификат и приватный ключ:

```bash
npm run bootstrap:cert
```

После этого еще раз пробуем запустить приложение.

Проект становится доступен по адресу: [https://localhost.msup.yandex-team.ru:8443/](https://localhost.msup.yandex-team.ru:8443/)  

### Переопределение хоста бэкенда
По-дефолту **WDS** ходит на localhost:8080, если нужен другой, то в .env.local меняет хост.

```bash
nano .env.local
# записать туда: https://cm-testing.market.yandex-team.ru/ в качестве бэкенда (в PROXY_HOST)
# и скопировать заголовок Cookie из браузера при обращении к нему (в COOKIE)
```

### Генерация definitions.ts:

- файл `java/definitions.ts` генерируется автоматически из SpringMVC контроллеров (т.е. правим контроллеры, запускаем команду ниже и TS соответствует бэкенду)
- Можно получить его с прода:

```bash
curl https://cm.market.yandex-team.ru/api/definitions.ts > src/java/definitions.ts
```

- Или с тестинга:

```bash
curl https://cm-testing.market.yandex-team.ru/api/definitions.ts > src/java/definitions.ts
```

- профит

### Локальное тестирование

```bash
npm run test
```
### Hermione тесты
На машине должна быть консольная утилита yav для доступа к секретнице https://vault-api.passport.yandex.net/docs
Нужно проставить в файле `.env.local` токен утилиты `HERMIONE_YAV_OAUTH_TOKEN`

```bash
npm run e2e
```

Для запуска локально или изменения конфигурации в дебаг-целях можно расширить конфиг гермионы создав файл 
`.hermione.conf.manual-extention.js`
и выставив в `.env.local`: `HERMIONE_USE_LOCAL_CONFIG=true`

Пример в файле: `.hermione.conf.manual-extention.sample.js`


### Выбор версии фронтенда
На s3 хранятся разные версии фронтенда КИ, собираемые в процессе прохождения покоммитных проверок (PR в гитхабе,
 тестовые сборки), и при выполнении пайплайна - прод версии. Типовые кейсы, когда это надо:

 - тестировщикам при тестировании новой версии, или просто кому-то предварительно показать. Заходим
https://cm-testing.market.yandex-team.ru/#/versions (или значок бранча слева от аватарки), 
выбираем нужную версию, жмем **"Установить локально"**. Выбранная версия загружается в **браузере**, значок бранча становится
желтеньким. После окончания тестирования жмем "Сбросить локальную версию".

- при необходимости откатить версию в проде. Заходим https://cm.market.yandex-team.ru/#/versions 
(или значок бранча слева от аватарки), выбираем нужную версию, жмем **"Форсировать глобально"**. 
Выбранная версия будет загружаться **у всех пользователей** КИ. После выкатки исправленной прод версии жмем
"Сбросить форсированную версию".

### Правки на фронте и бэке одновременно

Если так получилось, что надо одновременно поправить и фронт, и бэк. Рецепт в целом общий, здесь на примере
 отдельно поднятого МДМ. Допустим МДМ подняли на аиде, доступен вот так: http://aida.market.yandex.net:36501
* Не забываем взять новые definitions-mdm.ts с http://aida:36501/api/definitions.ts
* Идем в .mbocore.config.js, правим. Заголовки нужны для того, чтобы правильно работала авторизация(подставляем свои/нужные).
```js
  const apiDist = [
  '/auth',
  '/api',
  '/calendaring/',
  '/calendaring-service/',
  '/autoorder/',
  '/promo-management-api/',
  '/tolokaSettings',
  '/forecast-int',
]
  .map(path => {
    return {
      path,
      target: 'http://aida.market.yandex.net:36501',
      secure: false,
      changeOrigin: true,
      headers: process.env.COOKIE
        ? { Cookie: process.env.COOKIE }
        : {
          'User-login': 'your_login',
          'User-Roles': 'VIEWER',
        }, // So that it'll proxy Cookie header from browser
    };
  })
```
 * (Пере)запускаем npm start
 * После не забываем откатить изменения в .mbocore.config.js.

### Нюансы по пайплайну mbo-category-arc

В пайплайне [mbo-category-arc](https://tsum.yandex-team.ru/pipe/projects/mbo/delivery-dashboard/mbo-category-arc) 
есть кубики "Сборка фронтенда с тестовым definitions.ts", Тестирование фронтенда с тестовым definitions.ts. В них есть
параметр "Vcs Revision" выставленный в "9f89d499c80517cbe97dfe5fbadbd5af5ffbe574". Это не ошибка, это так задумано. 
Вкратце - пайплайн аркадийный, а джоба гитхабная. Вот их на этом vcs revision и скрещиваем. 
Если этого не сделать, TeamCity будет пытаться подтянуть ревизию текущей сборки Аркадии из гитхаба, которой там понятно
 нет. Симптомы - джоба висит в статусе "Requesting revision ..." и отваливается по таймауту.

#### Husky

В IDEA логи pre-push хука можно посмотреть на табе Console вкладки Git. При совсем непонятных ошибках может помочь:
```
npm ci && npm run prepare
```
Если надо отключить локально, к примеру опечатку в тексте правишь:
```
CI=1 git push
```
Либо переименовать .husky/pre-push, запушить, потом вернуть обратно
