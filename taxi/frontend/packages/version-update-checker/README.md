# version-update-checker

- [version-update-checker](#version-update-checker)
    - [Описание](#описание)
    - [Установка](#установка)
    - [Конфигурация](#конфигурация)
    - [Методы и свойства инстанса](#методы-и-свойства-инстанса)
    - [Использование](#использование)
    
### Описание

Утилита позволяет следить за обновлением версии приложения и запускать кастомную логику при обнаружении изменения версии

### Установка

`npm i -S version-update-checker`

### Конфигурация

| option                    | required |    type    |          default          |                                                                                                                                     description |
|:--------------------------|:--------:|:----------:|:-------------------------:|------------------------------------------------------------------------------------------------------------------------------------------------:|
| `url`                     |  `true`  |  `string`  |             -             |                                                                                      Путь, по которому нужно делать запрос для получения версии |
| `fetchOptions`            | `false`  |  `object`  |             -             |                                                                           Опции метода fetch для передачи дополнительных параметров при запросе |
| `versionFieldPath`        | `false`  |  `string`  |         `version`         |                    Путь до поля с версией сервиса в ответе на запрос в формате data.1.value (индекс элемента в массиве указывается через точку) |
| `checkInterval`           | `false`  |  `number`  |           `600`           |                                                                                                        Периодичность проверки версии в секундах |
| `initialVersion`          | `false`  |  `string`  |             -             |                                                                                       Версия, которая будет считаться текущей при инициализации |
| `isVersionsEqual`         | `false`  | `function` | Строгое сравнение (`===`) |                                              Функция сравнения двух версий. Первый аргумент – предыдущая версия, второй аргумент – новая версия |
| `handleVersionChange`     | `false`  | `function` |      Вывод в консоль      | Функция-обработчик, которая будет вызвана при обнаружении изменения версии. Первый аргумент – предыдущая версия, второй аргумент – новая версия |
| `handleVersionFetchError` | `false`  | `function` |      Вывод в консоль      |                            Функция-обработчик, которая будет вызвана при ошибке в запросе текущей версии. Принимает ошибку в качестве аргумента |

Пример:

```typescript
const config = {
    url: 'https://url/to/check/version',
    fetchOptions: {method: 'POST', body: JSON.stringify(serviceInfo)},
    versionFieldPath: 'data.configs.1.version',
    checkInterval: 30,
    initialVersion: '123',
    isVersionsEqual: (oldVer, newVer) => oldVer.split('.')[2] < newVer, 
    handleVersionChange: (oldVer, newVer) => `console.log`(`Предыдущая версия – ${oldVer}. Текущая версия – ${newVer}`),
    handleVersionFetchError: (error) => `console.log`('Ошибка в запросе версии: ', error)
}
```

### Методы и свойства инстанса

`currentVersion` – свойство хранит текущую версию

`start` – метод запускает проверку изменения версии

`stop` – метод останавливает проверку изменения версии

### Использование

```typescript
const service = new VersionUpdateChecker({
    url: 'https://url/to/check/version',
    handleVersionChange(oldVer, newVer) {
        alert(`${oldVer} -> ${newVer}`);
    }
});

service.start();
service.stop();
```