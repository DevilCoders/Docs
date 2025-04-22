# @yandex-int/messenger.decorators

![version](https://badger.yandex-team.ru/npm/@yandex-int/messenger.decorators/version.svg)<br>
[![dep health](https://oko.yandex-team.ru/badges/repo.svg?vcs=arc&repoName=frontend/packages/messenger.decorators)<br>
![dist health](https://oko.yandex-team.ru/badges/pkg.svg?pkgName=@yandex-int/messenger.decorators)
](https://oko.yandex-team.ru/repo/search-interfaces/frontend?repoFilter=packages/messenger.decorators)

## Install:

```
npm i @yandex-int/messenger.decorators --registry=http://npm.yandex-team.ru
```

## Methods

### - bind

Декоратор для установки контекста при вызове функции.
Установленный на методе класса позволяет внутри него в this всегда иметь текущий инстанс класса.

```
import { bind } from '@yandex-int/messenger.decorators'

class Foo {
    @bind
    bar() {
        this.key = 'val';
    }
}
```

### - attachRef

Пробрасывает ref элемента из рендера в свойство класса.

```
import { attachRef } from '@yandex-int/messenger.decorators'

interface FooProps {
    forwardedRef?: React.Ref<HTMLTextAreaElement>;
}

class Foo extends React.Component<FooProps> {
    @attachRef('forwardedRef')
    textareaRef: React.RefObject<HTMLTextAreaElement>;

    render() {
        return (
            <textarea ref={this.textareaRef} />
        );
    }
}
```
