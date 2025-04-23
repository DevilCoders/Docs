# Платформа экспериментов
Для нужд A/B тестирования мы ходим в платформу экспериментов - UserSplit.
На серверной части фронтэнда (jsx / node.js) есть настройка в конфиге `'user-split-url': 'http://uaas.search.yandex.net/mail'`.

UserSplit (он же UaaS) умеет разбивать по:
- `uid`-ам (передаётся в GET параметре `uuid`)
- по `yandexuid`-у (передаётся в заголовке с куками, см пример ниже)
- одновременно и по `uid`-у и по `yandexuid`-у

## Как это работает
- платформа экспериментов возвращает для пользователя набор ID-шников экспериментов
- в модуле [`jsx-common`](https://github.yandex-team.ru/daria/jsx) в `components/experiments.jsx` в обоих бранчах `ns` и `master` (если нужно, чтобы изменения применились и в Лизе и в Дарье, в будущем будет одна ветка) мы проверяем, что пользователь подходит по критериям под эксперимент
  - если подходит - возвращаем для него этот ID эксперимента
  - не подходит - не возвращаем
- в host-root в `index.jsx` мы
  - получаем все эксперименты, которые выдала платформа и которые подошли пользователю
  - если эксперимент для пользователя новый - проставляем для него настройки и сохраняем в настройках же, что эксперимент был применён (к примеру, если пользователю выпал эксперимент `24089` - после применения настроек проставляем пользователю также настройку `exp-24089-applied`, чтобы не применять настройки эксперимента повторно).

## Примеры запросов для разных видов разбиения

### По `uid`
```sh
$ curl -v 'http://uaas.search.yandex.net:80/mail?uuid=161105670'
< HTTP/1.1 200 Ok
< X-Yandex-RandomUID: 9211428051517392610
< X-Yandex-LogstatUID: 9211428051517392610
< X-Yandex-ExpConfigVersion: 7885
< X-Yandex-ExpBoxes: 63582,0,0;63735,0,13;53504,0,22;60671,0,96;55591,0,96
< X-Yandex-ExpFlags: W3siSEFORExF...fX19fV0=,W3siSEF...9fX19XQ==,W3siSEFORE...l19fX1d,W3siSEFOR...9Il19fX1d,W3siSEF...7fX19XQ==
< Content-Length: 9
<
* Connection #0 to host uaas.search.yandex.net left intact
* Closing connection #0
USERSPLIT
```

### По `yandexuid`
```sh
$ curl -v 'http://uaas.search.yandex.net:80/mail' -H 'cookie: yandexuid=5741465051512115103'
< HTTP/1.1 200 Ok
< X-Yandex-RandomUID: 8547732891517392282
< X-Yandex-LogstatUID: 5741465051512115103
< X-Yandex-ExpConfigVersion: 7885
< X-Yandex-ExpBoxes: 37396,0,98;64854,0,98;55589,0,34
< X-Yandex-ExpFlags: W3siSEFO...JwJyJ9XQ==,W3siSEFORExFUiI6ICJSRVB...X1d,W3siSEFORExFUiI6ICJNQUl...19XQ==
< Content-Length: 9
<
* Connection #0 to host uaas.search.yandex.net left intact
* Closing connection #0
USERSPLIT
```

### Когда ничего нет
В этом случае UaaS генерирует радномный `X-Yandex-RandomUID` и строит разбиение на его основе.
Это же значение можно выставлять пользователю в `yandexuid` куку, к примеру, но мы решили (в homer) сами генерировать `yandexuid` куку, поэтому у нас всегда что-то будет.

```sh
$ curl -v 'http://uaas.search.yandex.net:80/mail'
< HTTP/1.1 200 Ok
< X-Yandex-RandomUID: 2115220581517392133
< X-Yandex-LogstatUID: 2115220581517392133
< X-Yandex-ExpConfigVersion: 7885
< X-Yandex-ExpBoxes: 63581,0,56;64565,0,90;55592,0,90
< X-Yandex-ExpFlags: W3siSEFORExFUiI6IC...fX19fV0=,W3siSEFORExFUiI6ICJHQVR...fX19XQ==,W3siSEFORExFUiI6ICJNQUl...7fX19XQ==
< Content-Length: 9
<
* Connection #0 to host uaas.search.yandex.net left intact
* Closing connection #0
USERSPLIT
```

## Как проверять
**Важно**: внутри локальной сети Яндекса эксперименты могут не возвращаться (настраивается в платформе экспериментов).

В самой платформе экспериментов есть [глазик](https://jing.yandex-team.ru/files/eljusto/Slack_2016-06-30_11-56-24.png):
- если глазика нет, то на всех
- иначе - только на внешнюю сеть

### Параметры `experiments` и `experiments-json`

Для тестирования можно использовать GET параметры `experiments` и `experiments-json`.

```js
// Подробнее тут https://wiki.yandex-team.ru/pochta/experiments/readme/#testirovanie
// Примеры запросов:
verstka12-qa.yandex.ru/?experiments=26802,0,0;26805,0,0
verstka12-qa.yandex.ru/?experiments=34596,0,0&experiments-json=W3siSEFORExFUiI6Ik1BSUwiLCJDT05URVhUIjp7Ik1BSUwiOnsiZmxhZ3MiOlsie30iXX19fV0=
```

В реальности запрос за экспериментами выглядит примерно так (параметр `uuid` это не опечатка,
хотя туда передаётся обычный `uid`):
```
curl -v \
    -H 'User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10.11; rv:47.0) Gecko/20100101 Firefox/47.0' \
    -H 'X-Forwarded-For-Y: 213.180.219.181' \
    'http://uaas.search.yandex.net/mail?uuid=22805354'
```

Пример ответа:
```
< HTTP/1.1 200 Ok
< X-Yandex-RandomUID: 8074054731473679160
< X-Yandex-ExpConfigVersion: 5228
< X-Yandex-ExpBoxes: 27565,0,5;25467,0,13
< X-Yandex-ExpFlags: W3siSEFORExFUiI6ICJHQVRFV0FZIiwgIkNPTlRFWFQiOiB7IkdBVEVXQVkiOiB7InByZSI6IFsidHJ1ZSJdLCAiYXRvbS5wYXJhbXMucmVsZXYiOiBbImF0b21fcG9wdXBfc3RvcmVkLWNhbmRpZGF0ZS1saXN0PWltYWdlc19wb3B1cF9FWFBfcHJvZCJdfX0sICJDT05ESVRJT04iOiAiU0VTU0lPTl9hdG9tX2NsaWVudCA9PSAnaW1hZ2VzJyJ9XQ==,W3siSEFORExFUiI6ICJSRVBPUlQiLCAiQ09OVEVYVCI6IHsiUkVQT1JUIjogeyJ0ZXN0aWQiOiBbIjI1NDY3Il19LCAiTUFJTiI6IHt9fX1d
< X-Yandex-ExpConfigVersion-Pre: 5230
< X-Yandex-ExpBoxes-Pre: 27565,0,5;25467,0,13;30747,0,41
< X-Yandex-ExpFlags-Pre: W3siSEFORExFUiI6ICJHQVRFV0FZIiwgIkNPTlRFWFQiOiB7IkdBVEVXQVkiOiB7InByZSI6IFsidHJ1ZSJdLCAiYXRvbS5wYXJhbXMucmVsZXYiOiBbImF0b21fcG9wdXBfc3RvcmVkLWNhbmRpZGF0ZS1saXN0PWltYWdlc19wb3B1cF9FWFBfcHJvZCJdfX0sICJDT05ESVRJT04iOiAiU0VTU0lPTl9hdG9tX2NsaWVudCA9PSAnaW1hZ2VzJyJ9XQ==,W3siSEFORExFUiI6ICJSRVBPUlQiLCAiQ09OVEVYVCI6IHsiUkVQT1JUIjogeyJ0ZXN0aWQiOiBbIjI1NDY3Il19LCAiTUFJTiI6IHt9fX1d,W3siSEFORExFUiI6ICJNQUlMIiwgIkNPTlRFWFQiOiB7Ik1BSUwiOiB7fX19XQ==
< Content-Length: 9
```

Подробное описание заголовков есть на wiki https://wiki.yandex-team.ru/users/buryakov/usaas/.

Основное:
- `X-Yandex-ExpBoxes` - список троек `<test_id>,0,<bucket>`, разделённых `;`.
Здесь `<test_id>` - идентификатор эксперимента, `<bucket>` - номер бакета, в который попал пользователь. `0` - это атавизм номера слота, который сейчас не используется и оставлен лишь для совместимости с парсерами логов.
- `X-Yandex-ExpFlags` - список параметров экспериментов, разделённых запятой. Каждый из параметров есть закодированный base64 валидный json. Параметров может быть несколько, если пользователь попадает в несколько экспериментов одновременно.

В коде Лизы эксперименты доступны в `Daria.Config`:
- `exp-boxes` - полностью заголовок `X-Yandex-ExpBoxes`
- `eexp-boxes` - применённые эксперименты из загловка `X-Yandex-ExpBoxes`
- `exp-test-ids` - список ID примененных экспериментов

## Какие эксперименты настроены сейчас в платформе

Чтобы узнать, какие эксперименты в проде и с какими параметрами,
надо ходить в главный почтовый конфиг почты:
- https://ab.yandex-team.ru/config/56 - конфиг Mail
- выбираем последнюю версию, которая в проде https://jing.yandex-team.ru/files/chestozo/2016-09-09_12-28-40.png
- в конфиге видны все активные в данный момент эксперименты https://jing.yandex-team.ru/files/chestozo/2016-09-09_12-29-20.png

## Как посмотреть что за эксперимент по ID
https://ab.yandex-team.ru/testid/26801

## Разные полезные ссылки
- руководство по настройке экспериментов (по задаче https://st/DARIA-56933 Поддержка флагов) https://wiki.yandex-team.ru/Pochta/experiments/readme/
- описание UserSplit-а (платформы экспериментов) "Usersplit As A Service (UaaS) aka УАЗ" https://wiki.yandex-team.ru/users/buryakov/usaas/
- пример заведённого эксперимента про новый Приветственный Промо Визард в Лизе https://ab.yandex-team.ru/task/EXPERIMENTS-8113
- разные интересные таски
  - про то, как настраивать эксперименты с разбиением по `yandexuid` https://st.yandex-team.ru/DARIA-62704#1516198236000
  - про то, из-за чего может быть перекос в выборках (когда у эксперимента указано условие `desktop only`, но мобильные и планшеты всё равно приходят на сервис) https://st.yandex-team.ru/DARIA-62739#1516717090000
