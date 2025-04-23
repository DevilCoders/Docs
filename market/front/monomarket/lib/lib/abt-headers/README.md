[![oko health](https://oko.yandex-team.ru/badges/repo.svg?repoName=market/monomarket&vcs=github&repoFilter=lib/lib/abt-headers)](https://oko.yandex-team.ru/github/market/monomarket?repoFilter=lib/lib/abt-headers) [![oko health](https://oko.yandex-team.ru/badges/pkg.svg?pkgName=@yandex-market/abt-headers)](https://oko.yandex-team.ru/pkg/@yandex-market/abt-headers)

# `abt-headers`

Модуль для обработки заголовков [UaaS](https://wiki.yandex-team.ru/users/buryakov/usaas/).

## Инфо

-   [документация по экспериментальному модулю L7 балансера](https://wiki.yandex-team.ru/JandeksPoisk/Sepe/balancer/Cookbook/expdoc/);
-   [разбор экспериментальных заголовков](https://wiki.yandex-team.ru/SERP/development/UserSplit/).

## Логика работы

Типичный эксперимент фронтенда задаётся в админке экспериментов со следующей структурой:

```json
[
    {
        "HANDLER": "MARKET",
        "CONTEXT": {
            "DESKTOP": {
                "rearr": ["pepyakarearr=100"],
                "flags": ["flag_1=10", "flag_2"],
                "testid": ["33971"],
                "exprt": ["yametrika=1"]
            }
        }
    }
]
```

, где:

-   `HANDLER` — название скоупа экспериментов. По умолчанию `MARKET`;
-   `CONTEXT` — может содержать ключи с указанием платформы (базово: `DESKTOP` или `TOUCH`);
-   `CONTEXT.DESKTOP.rearr` — массив rearr-флагов (`"key=value"` или `"key"`). Пробрасываются на бэкенды;
-   `CONTEXT.DESKTOP.flags` — массив эксп-флагов фронтенда (`"key=value"` или `"key"`). Используются на фронтенде для включения функциональности экспериментов;
-   `CONTEXT.DESKTOP.testid` — id эксперимента;
-   `CONTEXT.DESKTOP.exprt` — массив доп. параметров эксперимента (`"key=value"`):
    -   `yametrika` — пробрасывать testid данного эксперимента в Метрику.
-   `CONTEXT.MARKETAPPS.alias` — аналог эксп флагов, только для приложений (`"key=value"`):

В случае с пересекающимися экспериментами, в заголовках может прилететь несколько base64-кодированных конфига.

Модуль:

-   декодирует эти значения (`base64-decode` + `JSON.parse`). При этом битое значение в одном из конфигов не потащит за собой остальные;
-   отфильтровывает конфиги с нужными значениями `HANDLER` и `CONTEXT`. Значения для `CONTEXT` можно указать несколько при вызове модуля;
-   производит merge значений конфигов:
    -   `rearr` — простой конкатенацией значений в массиве `rearrFlags`;
    -   `testid` — простой конкатенацией значений в массиве `testIds`;
    -   `flags` — конвертацией в объект, где ключом является строка до символа `=`, а значение вычисляется следующим образом:
        -   `true`, если `=` отсутствует (`my_flag`);
        -   строка после `=`, если она не является числом (`my_flag=abcd`);
        -   число после `=`, если там число (`my_flag=123.2`);
            В случае повторения ключей в различных экспериментах, значение будет присвоено от последнего;
-   из списка тест-бакетов `x-yandex-expboxes` отфильтровывает бакеты, `testid` которых не попал в текущую выборку конфигов.

## Пример использования

```typescript
import processAbtHeaders from '@yandex-market/abt-headers';

function abtMiddleware(req, res, next) {
    // Извлекаем конфиги с CONTEXT: 'DESKTOP'.
    const abtData = processAbtHeaders(req, ['DESKTOP']);

    // Были ли ошибки при парсинге заголовков.
    if (abtData.errors.length) {
        // Печатаем сырые заголовки.
        console.log(abtData.raw);

        // Логируем ошибки.
        console.error(abtData.errors);
    }

    req.abt = abtData;

    console.log(req.abt.expFlags); // -> {'flag_1': true, 'flag_2': 'abc'}
    // аналог expFlags для приложений
    console.log(req.abt.aliases); // -> {'alias_1': true, 'alias_2': 'abc'}
    console.log(req.abt.rearrFlags); // -> ['rearr_1=123', 'rearr2']
    console.log(req.abt.testIds); // -> ['1232213', '23432']
    console.log(req.abt.expBuckets); // -> '1232213,0,2;23432,0,-1'

    // testid для проброса в Метрику.
    console.log(req.abt.clientTestIds); // -> ['23432']

    next();
}
```

Также можно зафорсить установку эксп-флагов путём передачи дополнительного параметра.
В таком случае значения заголовков будут проигнорированы:

```typescript
import processAbtHeaders from '@yandex-market/abt-headers';

const abtData = processAbtHeaders(request, ['DESKTOP'], {
    forcedFlags: 'flag1;flag2=value2;flag3=3',
});

console.log(abtData.expFlags); // -> {'flag1': true, 'flag2': 'value2', 'flag3': 3}
console.log(abtData.rearrFlags); // -> {}
console.log(abtData.testIds); // -> {}
console.log(abtData.expBuckets); // -> ''
```
