# Написание кадавризированных тестов

Процесс написание непосредственно тестов, взаимодействующих с Кадавриком, по большей части схож с [обычным написанием hermione тестов](https://wiki.yandex-team.ru/Market/Verstka/HermioneCookBook/), за исключением некоторых моментов:

- **Обязательно** нужно указать окружение 'kadavr'
- Появляется возможность вызывать `this.browser.setState` для установки каких-либо тестовых данных, необходимых для работы моков бекендов
```javascript
makeCase({
  environment: 'kadavr',
  test() {
    return Promise
      .all([
        this.browser.setState('имя_коллекции1', require('./данные1.json')),
        this.browser.setState('имя_коллекции2', require('./данные2.json')),
      ])
      .then(() => {/* тест */});
 });
```
