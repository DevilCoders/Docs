StyleSelector
==========

Получает селектор, позволяющий получить доступ к элементу по хешу имени класса.

Использование:

```javascript
const {StyleSelector} = require('@self/project/src/utils/styleSelector');
const MyComponentStyleSelector = new StyleSelector('@self/project/src/components/MyComponent/styles.styl');

const rootClassSelector = MyComponentStyleSelector.root // [class*="COMPONENT_CLASS_HASH"]

```
