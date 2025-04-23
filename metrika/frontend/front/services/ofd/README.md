# ofd

### Подготовка

Для работы потребуется Node.js 10.

Для начала [устанавливаем Brew](https://wiki.yandex-team.ru/spec/devops/kakustanovitbrew/). Затем:

```bash
# Устанавливаем NVM (не забываем выполнить инструкции от Brew в секции Caveats)
brew install nvm

# Устанавливаем Node.js 10 версии
nvm install 10
```

### Секреты для локальной разработки
Секреты хранятся в специальном сервисе [секретница](https://yav.yandex-team.ru/edit/secret/sec-01d6jahbthrsmxgpmq5msyte4f)
Для старта разработки необходимо разложить секреты в два файлика - `.tvm.json` и `.local-dev-secrets.json`. Они добавлены в `.arcignore`.
1) Скопировать файл `.tvm-example.json` под именем `.tvm.json`. Вставить в поле `clients.ofd_frontend.secret` секрет из https://abc.yandex-team.ru/services/ofd/resources/?supplier=14&type=47&type=50&state=requested&state=approved&state=granted&view=consuming&show-resource=5463480
2) Скопировать файл .local-dev-secrets-example.json под именем .local-dev-secrets.json. Пока в приложении секретов нет.

### Установка и запуск

```bash
# Переходим в servises/ofd и устанавливаем зависимости
npm ci

# Запускаем приложение (magicdev запросит ваш пароль, чтобы запустить его на 443 порту).
# По необходимости, вы может задать другой порт, не требующий sudo, в файле .magicdev.json.
npm run dev
```
Проект становится доступен по адресу:
https://localhost.msup.yandex.ru/new

## Сборка и деплой

Сборка релиза в таске сандбокса [METRIKA_FRONTEND_RELEASE](https://sandbox.yandex-team.ru/task/463989697/view), параметры Сервис: ofd, Новый релиз: true

Проект находится в deploy: [тестовое окружение](https://deploy.yandex-team.ru/stages/ofd-testing) и [прод окружение](https://deploy.yandex-team.ru/stages/ofd-production)

### Доступные команды

Команда | Действие
------------ | -------------
dev | Запуск tvmtool и приложения для локальной разработки
build:production | Запуск production сборки скриптов и стилей
lint | Проверка TypeScript и CSS кода на codestyle

### Работа с компонентом `<I18n />`

* Оберните компонент для которого требуется получить локализованную строку в компонент `<I18n />`.
* Передайте компоненту `<I18n keyset={keyset} />` кейсет для поиска ключей.
* В качестве потомка создайте функцию, аргументом которой будет являться функция i18n от данного кейсета.
* Функция i18n принимает 2 параметра: название ключа и опциональные параметры, среди которых может быть параметр count, который используется для получения множественных форм.

```tsx
    /*
     * Директорию ./ExampleKeyset.i18n нужно создать при добавлении блока
     */
    import * as keyset from './ExampleKeyset.i18n';

    <I18n keyset={keyset}>
        {(i18n) => (
            <div>
                {i18n('test-key-with-params', {
                    paramName: 'testParam',
                    count: 10
                })}
            </div>
        )}
    </I18n>
```

* При необходимости, можно получить не локализованную строку, а исходный массив, содержащий части ключа и подставленный параметр. Для этого используйте компонент <I18nRaw />.

```tsx
    /*
     * Директория ./ExampleKeyset.i18n с содержимым формируется автоматически при выполнении npm run i18n:pull
     */
    import * as keyset from './ExampleKeyset.i18n';

    <I18nRaw keyset={keyset}>
        {(i18nRaw) => (
            <p>
                {i18nRaw('test-key-with-params', {
                    paramComponent: <Сomponent />
                })}
            </p>
        )}
    </I18nRaw>
```

### Документация

* [Гайды по использованию проектов на основе Project Stub](https://wiki.yandex-team.ru/toolbox/project-stub/)
