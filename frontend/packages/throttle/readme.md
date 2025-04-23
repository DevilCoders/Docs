# @yandex-int/throttle

![version](https://badger.yandex-team.ru/npm/@yandex-int/throttle/version.svg)<br>
[![dep health](https://oko.yandex-team.ru/badges/repo.svg?vcs=arc&repoName=frontend/packages/throttle)<br>
![dist health](https://oko.yandex-team.ru/badges/pkg.svg?pkgName=@yandex-int/throttle)
](https://oko.yandex-team.ru/repo/search-interfaces/frontend?repoFilter=packages/throttle)

## Install:

```
npm i @yandex-int/throttle --registry=http://npm.yandex-team.ru
```

## Methods

### - throttle

Метод для торможения вызова функции. Применяется для того, что бы вызывать функцию, переданную в него
не чаще указанного времени.

Например, вызов onChange поля input при быстром наборе.

```
import { throttle } from '@yandex-int/throttle'

const foo = throttle(handleChange, 500);
```

### - throttleRaf

Специальная версия для троттлинга функции Request Animation Frame в случае,
если функция для передачи в window.requestAnimationFrame работает заметно дольше,
чем минимальное время перересовки фрейма.

```
import { throttleRaf } from '@yandex-int/throttle'

const foo = throttleRaf(barFn);
```


### - throttleRafDecorator

Навешивает функцию на window.requestAnimationFrame и троттлит ее вызов

```
import { throttleRaf } from '@yandex-int/messenger.decorators'

class Foo {
    @throttleRaf
    adjustThrottle() {}

    @bind
    handleWindowResize() {
        this.adjustThrottle();
    }
}
```
