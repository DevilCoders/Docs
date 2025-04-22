StyleSelector
==========

Получает селектор, позволяющий получить доступ к элементу по хешу имени класса.

Использование:

```javascript
import {StyleSelector} from 'utils/styleSelector';
const MyComponentStyleSelector = new StyleSelector('@/components/MyComponent/styles.styl');

const rootClassSelector = MyComponentStyleSelector.root // [class*="COMPONENT_CLASS_HASH"]

```
