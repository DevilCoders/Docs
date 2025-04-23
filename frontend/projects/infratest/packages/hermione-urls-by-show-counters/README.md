# hermione-urls-by-show-counters

Плагин для [hermione](https://github.com/gemini-testing/hermione), позволяющий получать урлы, по которым была показана та или иная фича, используя её счетчик показа.

Добавляет в рантайм команду `getUrlsByShowCounter` следующей сигнатуры:
```
@param {String} counter - id счётчика показа
@param {String} [platform='desktop'] - платформа
@returns {String[]|undefined} - набор относительных url (e.g. '/search/touch/?text=test')
```

В данный момент команда работает для `web4` и следующих платформ:

* `desktop` (по умолчанию),
* `touch (touch-phone)`,
* `pad (touch-pad)`,
* `searchapp`.

## ВНИМАНИЕ!

Нет никаких гарантий, что команда вернёт урл, по которому действительно будет показана фича, потому что:

* По данной платформе фича с этим счетчиком ни разу не была показана за вчерашний день (тут проще, команда вернёт `undefined`);
* За время, прошедшее с момента сбора данных, фича уже успела устареть для данного запроса (см. колдунщики спортивных трансляций);
* Фича может работать только для залогинов, тогда в тесте придется авторизоваться в паспорте;
* Любые другие ограничения, не покрывающиеся только правильным url'ом;
* На момент конкретного открытия страницы гермионой, источник данных был недоступен.

## Установка

```bash
$ npm install @yandex-int/hermione-urls-by-show-counters --registry=http://npm.yandex-team.ru
```

## Использование

Необходимо подключить плагин в конфиге `hermione`:

```js
module.exports = {
    // ...

    plugins: {
        '@yandex-int/hermione-urls-by-show-counters': {
            enabled: true
        }
    },

    // ...
};
```

Здесь:

* `enabled` - плагин не делает ничего, если `enabled` установлен в `false`. По умолчанию равен `true`.

Пример использования команды в тесте:

```js
describe('Колдунщик матча - футбол', () => {
    it('Присутствует на выдаче', async function() {
        const counter = '/snippet/sport/livescore/football_match/before';
        const platform = 'desktop';
        const selector = '.sport-livescore';

        const checkUrl = async (url) => {
            await this.browser.url(url);

            const isVisible = await this.browser.isVisible(selector);
            if (!isVisible) {
                throw new Error(`Feature is not visible by url ${url}`);
            }
        };

        const urls = await this.browser.getUrlsByShowCounter(counter, platform);
        for (let url of urls) {
            await checkUrl(url);
        }
    });
});
```

## Подробности
Для работы используется пакет [urls-by-show-counters](https://github.yandex-team.ru/search-interfaces/infratest/tree/master/packages/urls-by-show-counters), в нем есть указания по настройке скачивания и использования ресурса.
