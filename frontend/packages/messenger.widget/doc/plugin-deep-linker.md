# Плагин для открытия виджета при клике на url мессенджера

Позволяет открывать ссылки мессенджера на сайте в виджете.
Плагин подписывается на CAPTURE фазу события `click`,
и в случае если target события - элемент `A` с `href` равным одному
из диплинков мессенджера - открывает виджет.

```ts
import { Widget, Config } from '@yandex-int/messenger.widget';
import { Deeplinker } from '@yandex-int/messenger.widget/plugins';

const widget = new Widget(new Config().create());

widget.addPlugin(new Deeplinker());
```

---