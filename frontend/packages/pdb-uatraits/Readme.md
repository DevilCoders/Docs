uatraits
========

 * https://wiki.yandex-team.ru/Morda/browserDetect/
 * https://github.yandex-team.ru/InfraComponents/uatraits
 * https://github.yandex-team.ru/InfraComponents/uatraits-data

Usage
-----

```js
var detect = require('@yandex-int/pdb-uatraits');

detect('Mozilla/5.0 (Linux; Android 4.1.2; Navigator Build/JZO54K) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/35.0.1916.141 Mobile Safari/537.36');
/*
{
      "isMobile": true,
      "isBrowser": true,
      "BrowserEngine": "WebKit",
      "BrowserEngineVersion": "537.36",
      "BrowserBase": "Chromium",
      "BrowserBaseVersion": "35.0.1916.141",
      "BrowserName": "ChromeMobile",
      "BrowserVersion": "35.0.1916",
      "isTablet": false,
      "OSFamily": "Android",
      "isTouch": true,
      "OSVersion": "4.1.2",
      "OSName": "Android Jelly Bean",
      "MultiTouch": true,
      "DeviceName": "Navigator",
      "DeviceModel": "Navigator"
}
*/
```

#### P.S.
1. В owners все, кто использовал pdb-uatraits из https://github.yandex-team.ru/pdb/pdb-uatraits
2. Тесты не работают, так как они не работали в GitHub
