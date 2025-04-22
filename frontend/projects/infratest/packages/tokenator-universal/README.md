# tokenator-universal

[![oko health](https://oko.yandex-team.ru/badges/pkg.svg?pkgName=@yandex-int/tokenator-universal)](https://oko.yandex-team.ru/pkg/@yandex-int/tokenator-universal)

Библиотека для работы с [OAuth-токенами](https://yandex.ru/dev/oauth/doc/dg/concepts/about.html). Получает токены пользователя для вашего приложения, в обмен на подпись SSH-ключом пользователя. Публичная часть ключа должна быть добавлена на Staff. Если какие-то токены есть в переменных окружения, будут использованы они.

## Установка

```
npm install @yandex-int/tokenator-universal
```

## Подключение

1. [Зарегистрируйте](https://oauth.yandex-team.ru/client/new) новое приложение в OAuth. В Callback URL укажите «URL для разработки». Отметьте галочками необходимые доступы.
2. Если нужно получать токены для Github Enterprise, [заведите](https://github.yandex-team.ru/settings/applications/new) новое приложение и там.
3. Подключите токенатор в коде, передав туда id и secret из пунктов выше:

```js
import tokenator from '@yandex-int/tokenator-universal';

const getTokens = tokenator({
  internal: {
    id: '<client_id_from_oauth>',
    secret: '<password_from_oauth>'
  },
  // Если нужен токен для Github Enterprise
  github: {
    id: '<client_id_from_github>',
    secret: '<secret_from_github>'
  }
});

const tokens = await getTokens(['sandbox', 'startrek']);
const sandboxToken = tokens.sandbox;
const startrekToken = tokens.startrek;
```

## Алгоритм работы

### При отсутствии ранее полученного токена
* проверяет наличие переменной окружения с нужным именем;
* в случае наличия – использует токен из неё, не проверяя его валидность;
* в случае отсутствия – получает новый токен автоматически.
### При наличии ранее полученного токена
* проверяет наличие переменной окружения с нужным именем;
* в случае наличия – использует токен из неё, не проверяя его валидность;
* в случае отсутствия – читает токен из файла с ранее полученными токенами (для внутренних сервисов также проверяется валидность токена);
* в любом случае – не пытается автоматически получить новый токен.

## Автоматическое получение токенов
Для получения токенов используются:
* для приложения [внутреннего OAuth](https://oauth.yandex-team.ru) используется [grant_type=ssh_key](https://wiki.yandex-team.ru/oauth/token/#granttypesshkey)
* для приложения [внутреннего Github](https://github.yandex-team.ru) используется [GitHub OAuth](https://developer.github.com/enterprise/2.11/apps/building-oauth-apps/authorizing-oauth-apps/).

Полученные токены сохраняются в файл в вашей домашней директории с правами на запись и чтение для текущего пользователя.

## Использование в различных окружениях
Сказанное выше подразумевает, что в Sandbox и Deploy вы должны полагаться **только** на токен в переменной окружения (именно поэтому токены регистрируются в `lib/tokens`).
Мы, конечно, могли бы настроить получение токенов по ssh-ключу зомбиков, но это:
1. Дополнительная настройка окружения;
2. Лишний http-запрос к `oauth.yandex-team.ru`.

## Возможные проблемы при автоматическом получении токена
* требует нужных скоупов в oauth-приложениях
  * [OAuth Internal](https://wiki.yandex-team.ru/oauth/token/#granttypesshkey),
  * [GitHub Enterprise](https://developer.github.com/enterprise/2.11/apps/building-oauth-apps/authorizing-oauth-apps/);
* требует наличия доступа по сети до `oauth.yandex-team.ru`/`github.yandex-team.ru`;
* требует настроенного `ssh-agent` и добавленных в него ключей – `ssh-add -l`;
* требует совпадения пользователя в системе и логина на стаффе (можно обойти, задав переменную окружения `STAFF_LOGIN`).

## Поддерживаемые сервисы
**NB:** Мы знаем, что для большинства внутренних сервисов можно использовать одинаковый токен, но, в силу поддержки не только локального окружения, токены сейчас регистрируются по отдельности.

Список сервисов смотрите в директории `src/services`.

Чтобы завести новые сервисы или изменить права существующих, необходимо:
1. Получить нужные гранты для вашего приложения [OAuth Internal](https://wiki.yandex-team.ru/oauth/token/#granttypesshkey) (нужно авторизоваться под соответствующим роботом);
2. Завести файл в `src/services` по аналогии с существующими.

## Принудительное переполучение токена
```bash
./bin/tokenator -f -t sandbox --internal-id <id> --internal_secret <secret>
```
Флаги для передачи id+secret для Internal Yandex сервисов: ```--internal-id <id> --internal-secret <secret>```

Флаги для передачи id+secret для Github: ```--github-id <id> --github-secret <secret>```

Несколько токенов указываются через запятую:
```bash
./bin/tokenator -f -t sandbox,startrek,github --internal-id <id> --internal-secret <secret> --github-id <id> --github-secret <secret>
```
Можно смотреть debug-вывод:
```bash
DEBUG='si:tokenator' ./bin/tokenator -f -t sandbox,startrek --internal-id <id> --internal-secret <secret>

```
