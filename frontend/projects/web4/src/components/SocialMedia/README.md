# SocialMedia

Блок, содержащий медиаконтент из социальных сетей, например, Instagram, Youtube, Twitter.

## Пример использования

```jsx
import React, { memo } from 'react';

import { SocialMedia } from '@components/SocialMedia/SocialMedia';
import { SocialMediaLogo } from '@components/SocialMedia/Logo';
import { SocialMediaPublicationThumb as PublicationThumb } from '@components/SocialMedia/PublicationThumb/SocialMediaPublicationThumb@desktop'

const Logo = <SocialMediaLogo type="instagram" />;

<SocialMedia
    title="Instagram"
    logo={Logo}
    url="https://www.instagram.com/gerardbutler/"
    username="gerardbutler"
>
    <PublicationThumb
        thumb="//avatars.mds.yandex.net/get-snippets_images/1961428/a8999dff645b4a8321e80ff3575c0577/desk_1x1_retina"
        url="https://www.instagram.com/p/CJbzGNLgEXN/"
    />
    <PublicationThumb
        thumb="//avatars.mds.yandex.net/get-snippets_images/1975454/e2a73dca5d2a652c17cd02911c6c8cce/desk_1x1_retina"
        url="https://www.instagram.com/p/CJML4HsAsrn/"
    />
    <PublicationThumb
        thumb="//avatars.mds.yandex.net/get-snippets_images/1966887/3b3179f24361a027c887777f3cc75d1f/desk_1x1_retina"
        url="https://www.instagram.com/p/CJJehRDA39s/"
    />
</SocialMedia>
```

`SocialMediaLogo` и `SocialMediaPublicationThumb` – дефолтные компоненты-обертки для более удобного использования, их можно заменить аналогичными компонентами, например, `Icon`, `Thumb`, `Topic` и т.п. для более гибкой сборки компонента.
