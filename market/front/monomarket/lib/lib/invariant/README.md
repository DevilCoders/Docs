[![oko health](https://oko.yandex-team.ru/badges/repo.svg?repoName=market/monomarket&vcs=github&repoFilter=lib/lib/invariant)](https://oko.yandex-team.ru/github/market/monomarket?repoFilter=lib/lib/invariant) [![oko health](https://oko.yandex-team.ru/badges/pkg.svg?pkgName=@yandex-market/invariant)](https://oko.yandex-team.ru/pkg/@yandex-market/invariant)

invariant
=========

Маленькая библиотека для [invariant-based programming](https://en.wikipedia.org/wiki/Invariant-based_programming).

Подробнее про кейсы почитать можно [здесь](https://docs.oracle.com/javase/7/docs/technotes/guides/language/assert.html).

Пример:
```js
import {invariant} from '@yandex-market/invariant';

invariant(42 === 0);
invariant(42 === 0, 'Ooops!');
```

Особенно полезно в сочетании с flow:
```js
declare function foo(string): void;
declare var kek: ?string;

test(kek);   // Err

invariant(kek != null);
test(kek);   // Ok
```

Обращаю внимание, что для flow необходимо, чтобы функция называлась `invariant`.
