# banner-system

Модуль для показана банеров.

## Использование

1. Создать баннерную систему

```ts
import { createBannerSystem } from '@client/shared/libs/banner-system';

export const bannerSystem = createBannerSystem('main');
```

2. Создать группу баннеров

Группа баннеров может иметь один из двух типов показа `display=one` или `display=all`.

Каждый баннер может обладать собственным весом `weight`, который будет учитываться при выборе баннера.

```ts
import { createBanner, createBannerGroup } from '@client/shared/libs/banner-system';

function useBannersData() {
  return useMemo(() => {
    const group = createBannerGroup({ display: 'one', key: 'store-key' });

    group.banners.push(createBanner({ id: 'banner-id', value: BannerComponent }));

    return group;
  }, []);
}
```

3. Подключить баннерную систему

```tsx
import { useBanner } from '@client/shared/libs/banner-system';

import { bannerSystem } from './banner-system';

const BannerTwister = () => {
  const data = useBannersData();
  const Banner = useBanner(bannerSystem, data);

  return <Banner />;
};
```

4. Подключить в баннер систему, для закрытия баннера

```tsx
import { bannerSystem } from './banner-system';

const BannerComponent = () => {
  const onDismiss = useEvent(bannerSystem.dismiss);

  return (
    <div>
      ...
      <Button onPress={onDismiss}>close</Button>
    </div>
  );
};
```

## Принцип работы

1. На основе веса определяется какой баннер будет показан.
1. Если группа баннеров обладает типом `display=all`, то баннеры будут показываться один за другим после закрытия.
1. Если группа баннеров обладает типом `display=one`, то будет показан один баннер, даже после закрытия.
1. После закрытия, в cookie (**на один день**) будет записан id закрытого банера и он не будет показан, пока время жизни cookie не истечет.
