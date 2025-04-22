# Apiary Migration Guide
 
## 0.14 - 1.0

### Определение статичности виджета

Статичность виджета теперь можно определить только в одном месте - в контроллере

*widgets/Foo/index.js:*
```diff
export default Widget.describe({
  name: '@widgets/Foo',
  view,
  controller,
- directives: {
-   static: true,
- }
});
```

*widgets/Foo/controller.js:*
```diff
export default () => {
  return {
    data: { ... },
+   static: true,
  };
}
```

### Статичность виджета в слоте

Возможность указать признак статичности для слота была удалена.
Вместо этого, указывайте признак статичности в самих виджетах, для которых вы создаете слоты.

*widgets/Foo/controller.js:*
```diff
- import {resolveExpFlagValueSync} from '@yandex-market/mandrel/resolvers/experiment';

export default (ctx: Context) => {
- const expStaticFlag = !resolveExpFlagValueSync(ctx, 'all_bar_static');

  return {
    slots: {
      header: Bar.create(ctx, { ... }, {
-       static: expStaticFlag,
      }),
    },
  };
};
```

*widgets/Bar/controller.js:*
```diff
+ import {resolveExpFlagValueSync} from '@yandex-market/mandrel/resolvers/experiment';

export default (ctx: Context) => {
+ const expStaticFlag = !resolveExpFlagValueSync(ctx, 'all_bar_static');

  return {
    data: { ... },
+   static: expStaticFlag,
  };
};
``` 
