# Плагин для открытия нативного мессенджера в мобильных ПП и Ябро

В случаее если браузер (мобильные ПП и Ябро) поддерживает диплинки мессенджера
вместо виджета будет открыт нативный мессенджер.

Нативный мессенджер не поддерживает api и события виджета, поэтому подходит только
в случае если использовать их не планируется.

```ts
import { Widget, Config } from '@yandex-int/messenger.widget';
import { NativeInterceptor } from '@yandex-int/messenger.widget/plugins';

const widget = new Widget(new Config().create());

widget.addPlugin(new NativeInterceptor());
```

---