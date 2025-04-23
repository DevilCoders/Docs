<style>
code {
  width: 450px;
  display: block;
}
code.inlined {
  width: auto;
  display: inline;
}
</style>
<table>
<thead>
    <tr>
        <th>Флаг</th><th>Тип</th><th>По-умолчанию</th><th>Описание</th>
    </tr>
</thead>
<tbody>
<tr>
<td>

```json
{
  "yandexTvGeneral": {
    "aliceUrl": ""
  }
}
```

</td>
<td>

String

</td>
<td>




</td>
<td>

[TVANDROID-6035](https://st.yandex-team.ru/TVANDROID-6035)

</td>
</tr>
<tr>
<td>

```json
{
  "yandexTvGeneral": {
    "marketUrl": "https://updater.mobile.yandex.net"
  }
}
```

</td>
<td>

String

</td>
<td>


https://updater.mobile.yandex.net

</td>
<td>

[TVANDROID-6475](https://st.yandex-team.ru/TVANDROID-6475)
<br><code class="inlined">marketUrl</code>:<br> - прод - "https://updater.mobile.yandex.net"<br>тестинг - "https://updater.infra.mobile.yandex.net"
</td>
</tr>
<tr>
<td>

```json
{
  "droidekaUrl": ""
}
```

</td>
<td>

String

</td>
<td>




</td>
<td>

[TVANDROID-4546](https://st.yandex-team.ru/TVANDROID-4546)
<br><code class="inlined">droidekaUrl</code>:<br> - престейбл - <code class="inlined">https://droideka.pre.smarttv.yandex.net</code><br>тестинг - <code class="inlined">https://droideka.tst.smarttv.yandex.net</code><br>прод - <code class="inlined">https://droideka.smarttv.yandex.net</code>
</td>
</tr>
<tr>
<td>

```json
{
  "yandexTvGeneral": {
    "yandexConnectivityCheckUrl": "http://www.google.com/generate_204"
  }
}
```

</td>
<td>

String

</td>
<td>


http://www.google.com/generate_204

</td>
<td>

[TVANDROID-6046](https://st.yandex-team.ru/TVANDROID-6046)
<br><code class="inlined">yandexConnectivityCheckUrl</code>:<br> - Переключать можно на яндексовую <code class="inlined">http://scbh.yandex.net/generate_204</code>
</td>
</tr>
<tr>
<td>

```json
{
  "networkMetricaLoggingEnabled": true
}
```

</td>
<td>

Boolean

</td>
<td>


true

</td>
<td>

[TVANDROID-4613](https://st.yandex-team.ru/TVANDROID-4613)

</td>
</tr>
<tr>
<td>

```json
{
  "yandexTvGeneral": {
    "dnsFallbackEnabled": false,
    "dnsFallbackWhitelist": [],
    "certificatesFallbackEnabled": false,
    "rootFallbackCerts": []
  }
}
```

</td>
<td>

Boolean<br>List<String><br>Boolean<br>List<String>

</td>
<td>


<br>["yandex.ru", "yandex.net"]<br>false<br>

</td>
<td>

[TVANDROID-5910](https://st.yandex-team.ru/TVANDROID-5910)
<br><code class="inlined">dnsFallbackEnabled</code>:<br> - включает использование https://wiki.yandex-team.ru/users/viktor-reznik/podderzhka-yandex-dns-v-kachestve-follbeka-sistemnomu-dns-v-okhttp/ в апдейтере для походов во все ручки. Может быть использовано и в других местах, код встроен в <code class="inlined">common:network</code><br><code class="inlined">dnsFallbackWhitelist</code>:<br> - необязательный, эффективен только с <code class="inlined">dnsFallbackEnabled</code><br>Список хостов, для использования YandexDns, если основной их не зарезолвил<br><code class="inlined">certificatesFallbackEnabled</code>:<br> - Включает доверие дополнительным рутовым сертификатам. По дефолту - серту минцифры.<br><code class="inlined">rootFallbackCerts</code>:<br> - необязательный, эффективен только с certificatesFallbackEnable=true.<br>Содержит Base64-encoded сертификаты, которым доверяем в апдейтере (возможно использование и в других приложениях).
</td>
</tr>

<tr>
<td>

```json
{
  "yandexTvGeneral": {
    "statisticsViewOnScreenMinPercent": "0.5",
    "statisticsViewOnScreenTimeoutMs": 300
  }
}
```

</td>
<td>

Double<br>Long

</td>
<td>


0.5<br>300

</td>
<td>

[TVANDROID-6004](https://st.yandex-team.ru/TVANDROID-6004)

</td>
</tr>

<tr>
<td>

```json
{
  "ott": {
    "ott_service_id": 167,
    "ott_service_name": "ya-tv-android"
  }
}
```

</td>
<td>

Int<br>String

</td>
<td>


167<br>ya-tv-android

</td>
<td>

[TVANDROID-5002](https://st.yandex-team.ru/TVANDROID-5002)

</td>
</tr>
<tr>
<td>

```json
{
  "ott": {
    "platformType": "",
    "platformName": "",
    "platformOs": "",
    "platformVersion": "",
    "platformModel": "",
    "platformVendor": ""
  }
}
```

</td>
<td>

String<br>String<br>String<br>String<br>String<br>String

</td>
<td>


<br><br><br><br><br>

</td>
<td>

[TVANDROID-5093](https://st.yandex-team.ru/TVANDROID-5093)

</td>
</tr>
<tr>
<td>

```json
{
  "ott": {
    "strmFrom": "tvandroid",
    "videosearchClient": "tvandroid",
    "objectsearchClient": "tvandroid"
  }
}
```

</td>
<td>

String<br>String<br>String

</td>
<td>


tvandroid<br>tvandroid<br>tvandroid

</td>
<td>

[TVANDROID-5070](https://st.yandex-team.ru/TVANDROID-5070)

</td>
</tr>
<tr>
<td>

```json
{
  "ott": {
    "strmFromRestApiHeader": "tvandroid"
  }
}
```

</td>
<td>

String

</td>
<td>


tvandroid

</td>
<td>

[TVANDROID-6095](https://st.yandex-team.ru/TVANDROID-6095)
<br><code class="inlined">strmFromRestApiHeader</code>:<br> - То же, что <code class="inlined">ott:strmFrom</code>, но только для REST API заголовка X-StrmFrom
</td>
</tr>

<tr>
<td>

```json
{
  "com.yandex.tv.daydream": {
    "screenSaverConfig": {
      "videoConfig": "",
      "imageConfig": ""
    }
  }
}
```

</td>
<td>

[MediaConfig](./types/com.yandex.tv.daydream.config.ScreenSaverConfigInfo.MediaConfig.md)<br>[MediaConfig](./types/com.yandex.tv.daydream.config.ScreenSaverConfigInfo.MediaConfig.md)

</td>
<td>


<br>

</td>
<td>

[TVANDROID-6463](https://st.yandex-team.ru/TVANDROID-6463)
<br><code class="inlined">videoConfig</code>:<br> - Конфиг для видео-скринсейвера<br><code class="inlined">imageConfig</code>:<br> - Конфиг для скринсейвера с картинками (на данный момент не используется)
</td>
</tr>

<tr>
<td>

```json
{
  "com.yandex.tv.home": {
    "catalogScreen": {
      "enable": false
    }
  }
}
```

</td>
<td>

Boolean

</td>
<td>


false

</td>
<td>

[TVANDROID-5141](https://st.yandex-team.ru/TVANDROID-5141)

</td>
</tr>
<tr>
<td>

```json
{
  "com.yandex.tv.home": {
    "contentStateManager": {
      "invalidationEnabled": false
    }
  }
}
```

</td>
<td>

Boolean

</td>
<td>


false

</td>
<td>

[TVANDROID-5879](https://st.yandex-team.ru/TVANDROID-5879)
<br><code class="inlined">invalidationEnabled</code>:<br> - Включение инвалидации контента с помощью новой архитектуры
</td>
</tr>
<tr>
<td>

```json
{
  "com.yandex.tv.home": {
    "contentStateManager": {
      "categoriesEnabled": false
    }
  }
}
```

</td>
<td>

Boolean

</td>
<td>


false

</td>
<td>

[TVANDROID-5880](https://st.yandex-team.ru/TVANDROID-5880)
<br><code class="inlined">categoriesEnabled</code>:<br> - Включение загрузки категорий с помощью новой архитектуры (используется вместе с флагом invalidationEnabled)
</td>
</tr>
<tr>
<td>

```json
{
  "com.yandex.tv.home": {
    "detailsScreenVideoPreviewV2": {
      "enabled": false,
      "volume": 0,
      "repeatEnabled": false
    }
  }
}
```

</td>
<td>

Boolean<br>Int<br>Boolean

</td>
<td>


false<br>0<br>false

</td>
<td>

[TVANDROID-5334](https://st.yandex-team.ru/TVANDROID-5334)
<br><code class="inlined">enabled</code>:<br> - включение/отключение трейлера<br><code class="inlined">volume</code>:<br> - громкость видео (0 - без звука, 100 - максимальная громкость)<br><code class="inlined">repeatEnabled</code>:<br> - включение зацикливания трейлера, при отключении, после завершения трейлер меняется на обложку
</td>
</tr>
<tr>
<td>

```json
{
  "com.yandex.tv.home": {
    "detailsExternalOptionsEnabled": false
  }
}
```

</td>
<td>

Boolean

</td>
<td>


false

</td>
<td>

[TVANDROID-5675](https://st.yandex-team.ru/TVANDROID-5675)

</td>
</tr>
<tr>
<td>

```json
{
  "com.yandex.tv.home": {
    "favoriteEnabled": false
  }
}
```

</td>
<td>

Boolean

</td>
<td>


false

</td>
<td>

[TVANDROID-5788](https://st.yandex-team.ru/TVANDROID-5788)

</td>
</tr>
<tr>
<td>

```json
{
  "com.yandex.tv.home": {
    "halfPirateDetailsEnabled": false
  }
}
```

</td>
<td>

Boolean

</td>
<td>


false

</td>
<td>

[TVANDROID-5896](https://st.yandex-team.ru/TVANDROID-5896)

</td>
</tr>
<tr>
<td>

```json
{
  "com.yandex.tv.home": {
    "json_high_priority_thread_parsing_enabled": false,
    "json_vanilla_parser_enabled": false
  }
}
```

</td>
<td>

Boolean<br>Boolean

</td>
<td>


false<br>false

</td>
<td>

[TVANDROID-4721](https://st.yandex-team.ru/TVANDROID-4721)

</td>
</tr>
<tr>
<td>

```json
{
  "com.yandex.tv.home": {
    "searchGrpcTestEnabled": false
  }
}
```

</td>
<td>

Boolean

</td>
<td>


false

</td>
<td>

[TVANDROID-6139](https://st.yandex-team.ru/TVANDROID-6139)

</td>
</tr>
<tr>
<td>

```json
{
  "com.yandex.tv.home": {
    "detailsCardGrpcSourceEnabled": false
  }
}
```

</td>
<td>

Boolean

</td>
<td>


false

</td>
<td>

[TVANDROID-5938](https://st.yandex-team.ru/TVANDROID-5938)

</td>
</tr>
<tr>
<td>

```json
{
  "com.yandex.tv.home": {
    "homeCarouselsGrpcEnabled": false
  }
}
```

</td>
<td>

Boolean

</td>
<td>


false

</td>
<td>

[TVANDROID-5776](https://st.yandex-team.ru/TVANDROID-5776)

</td>
</tr>
<tr>
<td>

```json
{
  "com.yandex.tv.home": {
    "fullscreenPromo": false,
    "fullscreenPromoAutoplayIntervalMs": 12000
  }
}
```

</td>
<td>

Boolean<br>Long

</td>
<td>


false<br>12000

</td>
<td>

[TVANDROID-5697](https://st.yandex-team.ru/TVANDROID-5697)
<br><code class="inlined">fullscreenPromo</code>:<br> - включает фулскрин-промоблок на домашнем экране<br><code class="inlined">fullscreenPromoAutoplayIntervalMs</code>:<br> - время автоперелистывания элементов промоблока в мс. Автоперелистывание включено, если <code class="inlined"> fullscreenPromoAutoplayIntervalMs > 0</code>
</td>
</tr>
<tr>
<td>

```json
{
  "com.yandex.tv.home": {
    "hideContinueWatchingCarouselTitles": false,
    "showRecentInsideContinueWatching": false,
    "recentInsideContinueWatchingPosition": 0,
    "recentInsideContinueWatchingSize": 6
  }
}
```

</td>
<td>

Boolean<br>Boolean<br>Int<br>Int

</td>
<td>


false<br>false<br>0<br>6

</td>
<td>

[TVANDROID-5580](https://st.yandex-team.ru/TVANDROID-5580)

</td>
</tr>
<tr>
<td>

```json
{
  "com.yandex.tv.home": {
    "showRecentIfNoContinueWatching": false
  }
}
```

</td>
<td>

Boolean

</td>
<td>


false

</td>
<td>

[TVANDROID-6093](https://st.yandex-team.ru/TVANDROID-6093)

</td>
</tr>
<tr>
<td>

```json
{
  "com.yandex.tv.home": {
    "isContinueWatchingDurationBadgeHiddenOutOfFocus": false,
    "isContinueWatchingProgressBackgroundEnabled": false
  }
}
```

</td>
<td>

Boolean<br>Boolean

</td>
<td>


false<br>false

</td>
<td>

[TVANDROID-5843](https://st.yandex-team.ru/TVANDROID-5843)

</td>
</tr>
<tr>
<td>

```json
{
  "com.yandex.tv.home": {
    "recentShowKinopoisk": true
  }
}
```

</td>
<td>

Boolean

</td>
<td>


true

</td>
<td>

[TVANDROID-5980](https://st.yandex-team.ru/TVANDROID-5980)

</td>
</tr>
<tr>
<td>

```json
{
  "com.yandex.tv.home": {
    "loginwallPolicy": {
      "storeAccessible": true,
      "profilesAccessible": true
    }
  }
}
```

</td>
<td>

Boolean<br>Boolean

</td>
<td>


true<br>true

</td>
<td>

[TVANDROID-5797](https://st.yandex-team.ru/TVANDROID-5797)

</td>
</tr>
<tr>
<td>

```json
{
  "com.yandex.tv.home": {
    "loginwallPolicy": {
      "appsAccessible": true,
      "youtubeAccessible": true
    }
  }
}
```

</td>
<td>

Boolean<br>Boolean

</td>
<td>


true<br>true

</td>
<td>

[YATV-64](https://st.yandex-team.ru/YATV-64)

</td>
</tr>
<tr>
<td>

```json
{
  "com.yandex.tv.home": {
    "reportMobileVelocityIndex": false
  }
}
```

</td>
<td>

Boolean

</td>
<td>


false

</td>
<td>

[TVANDROID-6480](https://st.yandex-team.ru/TVANDROID-6480)
<br><code class="inlined">reportMobileVelocityIndex</code>:<br> - Включает отправку метрик для подсчета MobileVelocityIndex
</td>
</tr>
<tr>
<td>

```json
{
  "com.yandex.tv.home": {
    "profileButtonWithAvatarEnabled": false
  }
}
```

</td>
<td>

Boolean

</td>
<td>


false

</td>
<td>

[TVANDROID-5453](https://st.yandex-team.ru/TVANDROID-5453)

</td>
</tr>
<tr>
<td>

```json
{
  "com.yandex.tv.home": {
    "pimpleOnProfileButtonEnabled": false
  }
}
```

</td>
<td>

Boolean

</td>
<td>


false

</td>
<td>

[TVANDROID-5703](https://st.yandex-team.ru/TVANDROID-5703)

</td>
</tr>
<tr>
<td>

```json
{
  "com.yandex.tv.home": {
    "screenSaverShortcutSettings": {
      "enabled": false,
      "mode": "doubleTap",
      "doubleTapInterval": 500,
      "longPressInterval": 2000
    }
  }
}
```

</td>
<td>

Boolean<br>String<br>Long<br>Long

</td>
<td>


false<br>doubleTap<br>500<br>2000

</td>
<td>

[TVANDROID-5920](https://st.yandex-team.ru/TVANDROID-5920)
<br><code class="inlined">mode</code>:<br> - can be one of <code class="inlined">singleTap</code>/<code class="inlined">doubleTap</code>/<code class="inlined">longPress</code>
</td>
</tr>
<tr>
<td>

```json
{
  "com.yandex.tv.home": {
    "searchTopTenConfig": "remote"
  }
}
```

</td>
<td>

String

</td>
<td>


remote

</td>
<td>

[TVANDROID-5665](https://st.yandex-team.ru/TVANDROID-5665)
<br><code class="inlined">searchTopTenConfig</code>:<br> - Can be one of <code class="inlined">nothing</code>/<code class="inlined">remote</code>/<code class="inlined">carousel</code>
</td>
</tr>
<tr>
<td>

```json
{
  "com.yandex.tv.home": {
    "showCategoriesPromoDot": ""
  }
}
```

</td>
<td>

String

</td>
<td>




</td>
<td>

[TVANDROID-4499](https://st.yandex-team.ru/TVANDROID-4499)

</td>
</tr>
<tr>
<td>

```json
{
  "com.yandex.tv.home": {
    "tandem": {
      "backgrounds": "{}"
    },
    "tandemColorCodesConfig": "{}"
  }
}
```

</td>
<td>

Object<br>Object

</td>
<td>


{}<br>{}

</td>
<td>

[TVANDROID-4872](https://st.yandex-team.ru/TVANDROID-4872)

</td>
</tr>
<tr>
<td>

```json
{
  "com.yandex.tv.home": {
    "nonTifInputIdsForVertical": []
  }
}
```

</td>
<td>

List<String>

</td>
<td>


Для Hisi351 ["hisi_351"], для остальных []

</td>
<td>

[TVANDROID-3907](https://st.yandex-team.ru/TVANDROID-3907)

</td>
</tr>
<tr>
<td>

```json
{
  "com.yandex.tv.home": {
    "useTvRubricator2": false
  }
}
```

</td>
<td>

Boolean

</td>
<td>


false

</td>
<td>

[TVANDROID-4390](https://st.yandex-team.ru/TVANDROID-4390)

</td>
</tr>
<tr>
<td>

```json
{
  "com.yandex.tv.home": {
    "searchVideoScenarioEnabled": false
  }
}
```

</td>
<td>

Boolean

</td>
<td>


false

</td>
<td>

[MODULE-28](https://st.yandex-team.ru/MODULE-28)

</td>
</tr>

<tr>
<td>

```json
{
  "test_ids": ""
}
```

</td>
<td>

String

</td>
<td>




</td>
<td>

[TVANDROID-3127](https://st.yandex-team.ru/TVANDROID-3127)

</td>
</tr>
<tr>
<td>

```json
{
  "env": {
    "testids": "",
    "test_buckets": ""
  }
}
```

</td>
<td>

String<br>String

</td>
<td>


<br>

</td>
<td>

[TVANDROID-5902](https://st.yandex-team.ru/TVANDROID-5902)

</td>
</tr>
<tr>
<td>

```json
{
  "appmetrikaReportEnvironment": "",
  "com.yandex.tv.services": {
    "metricaExperimentsEventDisabled": false
  }
}
```

</td>
<td>

String<br>Boolean

</td>
<td>


<br>false

</td>
<td>

[TVANDROID-6351](https://st.yandex-team.ru/TVANDROID-6351)
<br><code class="inlined">appmetrikaReportEnvironment</code>:<br> - Содержит одноуровневый json, который кладется в appmetrica environment<br>(флаг был и ранее, но в тв не использовался)<br><code class="inlined">metricaExperimentsEventDisabled</code>:<br> - Отключает поход в ручку дроидеки experiments и отсылку события метрики experiments
</td>
</tr>

<tr>
<td>

```json
{
  "com.yandex.tv.services": {
    "aliceBillingGiftDisabled": false
  }
}
```

</td>
<td>

Boolean

</td>
<td>


false

</td>
<td>

[TVANDROID-4795](https://st.yandex-team.ru/TVANDROID-4795)
<br><code class="inlined">aliceBillingGiftDisabled</code>:<br> - Получение карт пользователей и измененный флоу подарка<br>По дефолту новое получение подарка включено на тв и на модуле
</td>
</tr>

<tr>
<td>

```json
{
  "com.yandex.tv.services": {
    "iosdkWakeUpInterval": 1200000
  }
}
```

</td>
<td>

Long

</td>
<td>


1200000

</td>
<td>

[TVANDROID-4290](https://st.yandex-team.ru/TVANDROID-4290)

</td>
</tr>
<tr>
<td>

```json
{
  "com.yandex.tv.services": {
    "appUsageWakeupInterval": 10800000
  }
}
```

</td>
<td>

Long

</td>
<td>


10800000

</td>
<td>

[TVANDROID-4438](https://st.yandex-team.ru/TVANDROID-4438)
<br><code class="inlined">appUsageWakeupInterval</code>:<br> - Интервал в который запрашиваем из системы статистику по использованию апп. Если <= 0, будет использоваться старый механизм (неточный).
</td>
</tr>
<tr>
<td>

```json
{
  "com.yandex.tv.services": {
    "giftPromoLackTtl": 3600000,
    "giftPromoTimeout": 604800000,
    "giftPromoMaxCount": 3
  }
}
```

</td>
<td>

Long<br>Long<br>Int

</td>
<td>


3600000<br>604800000<br>3

</td>
<td>

[TVANDROID-5194](https://st.yandex-team.ru/TVANDROID-5194)
<br><code class="inlined">giftPromoLackTtl</code>:<br> - Через сколько вновь идем за подарком на бекенд, если его не было для этого устройства.<br><code class="inlined">giftPromoTimeout</code>:<br> - Минимальный таймаут между показами<br><code class="inlined">giftPromoMaxCount</code>:<br> - Максимальное количество показов промо подарка на устройство
</td>
</tr>
<tr>
<td>

```json
{
  "com.yandex.tv.services": {
    "timePersistConfig": ""
  }
}
```

</td>
<td>

[TimePersistConfig](./types/com.yandex.tv.services.TimePersistConfig.md)

</td>
<td>




</td>
<td>

[TVANDROID-6400](https://st.yandex-team.ru/TVANDROID-6400)

</td>
</tr>
<tr>
<td>

```json
{
  "com.yandex.tv.services": {
    "debugPanel": {
      "metricaLogging": false
    }
  }
}
```

</td>
<td>

Boolean

</td>
<td>


false

</td>
<td>

[TVANDROID-6248](https://st.yandex-team.ru/TVANDROID-6248)
<br><code class="inlined">metricaLogging</code>:<br> - [Debug builds only] Enables metrica events and environment logging via DebugPanelContentProvider and to file on diskon path . 
</td>
</tr>

<tr>
<td>

```json
{
  "experiments": []
}
```

</td>
<td>

List

</td>
<td>


[]

</td>
<td>

[TVANDROID-5166](https://st.yandex-team.ru/TVANDROID-5166)

</td>
</tr>
<tr>
<td>

```json
{
  "com.yandex.io.sdk": {
    "reportedPackages": {
      "include": []
    }
  }
}
```

</td>
<td>

List<[PackageLaunchInfo](./types/com.yandex.io.sdk.packages.ReportedPackagesConfig.PackageLaunchInfo.md)>

</td>
<td>




</td>
<td>

[TVANDROID-5316](https://st.yandex-team.ru/TVANDROID-5316)

</td>
</tr>
<tr>
<td>

```json
{
  "targetQuasar": "prod"
}
```

</td>
<td>

String

</td>
<td>


prod

</td>
<td>

[TVANDROID-4919](https://st.yandex-team.ru/TVANDROID-4919)
<br><code class="inlined">targetQuasar</code>:<br> - ИСПОЛЬЗОВАТЬ ОСТОРОЖНО<br>Флаг выставляет значение url quasar и billing бэкендов<br>prod - https://quasar.yandex.net<br>testing - https://quasar.yandex.net/dev<br>localhost - http://localhost:8888 (для автотестов, чтобы мокать получение подарка)<br>Иметь ввиду: ваш девайс должен быть прописан и в тестовой и в продовой админках (например, для модуля, тут https://quasmodrom-test.quasar-int.yandex-team.ru/quasarbackend/device и тут https://quasmodrom.quasar.yandex-team.ru/quasarbackend/device/) и в обоих должен быть конфиг.<br>При получении флага рекомендуется проверить и продовый и тестовый конфиг (чтобы не было ситуациации постоянного переключения).<br>Работает только на не-юзер билдах.<br>После применения флага рекомендуется перезагрузка.
</td>
</tr>
<tr>
<td>

```json
{
  "com.yandex.io.sdk": {
    "mordoviaHandler": {
      "enabled": true
    }
  }
}
```

</td>
<td>

Boolean

</td>
<td>


true

</td>
<td>

[TVANDROID-NONE](https://st.yandex-team.ru/TVANDROID-NONE)
<br><code class="inlined">enabled</code>:<br> - Настройки для iosdk-app mordoviaHandler.enabled == false выключает трансформацию для мордовийных комманд mordovia_show и mordovia_command в go_home.
</td>
</tr>
<tr>
<td>

```json
{
  "com.yandex.io.sdk": {
    "tandemSettingsEnabled": false
  }
}
```

</td>
<td>

Boolean

</td>
<td>


false

</td>
<td>

[TVANDROID-5115](https://st.yandex-team.ru/TVANDROID-5115)
<br><code class="inlined">tandemSettingsEnabled</code>:<br> - Включает управление тандемом через настройки.
</td>
</tr>
<tr>
<td>

```json
{
  "com.yandex.io.sdk": {
    "platformsAvailableToTandem": []
  }
}
```

</td>
<td>

List<String>

</td>
<td>


[yandexstation, yandexstation_2, yandexmini, yandexmini_2, yandexmicro, yandexmidi]

</td>
<td>

[TVANDROID-5280](https://st.yandex-team.ru/TVANDROID-5280)

</td>
</tr>

<tr>
<td>

```json
{
  "com.yandex.tv.services.platform": {
    "adbEnabled": false,
    "developmentSettingsEnabled": false
  }
}
```

</td>
<td>

Boolean<br>Boolean

</td>
<td>


false<br>false

</td>
<td>

[TVANDROID-4609](https://st.yandex-team.ru/TVANDROID-4609)

</td>
</tr>
<tr>
<td>

```json
{
  "com.yandex.tv.services.platform": {
    "disableMediaSkippableFragments": false,
    "disableMediaMetaForNextItem": false
  }
}
```

</td>
<td>

Boolean<br>Boolean

</td>
<td>


false<br>false

</td>
<td>

[TVANDROID-4884](https://st.yandex-team.ru/TVANDROID-4884)
<br><code class="inlined">disableMediaSkippableFragments</code>:<br> - Выключение отправки доп.инфы о skippableFragments (титры, заставка) проигрываемого видео<br><code class="inlined">disableMediaMetaForNextItem</code>:<br> - Выключение отправки доп.инфы о проигрываемом видео, нужной для включения следующего видео (серии)
</td>
</tr>
<tr>
<td>

```json
{
  "com.yandex.tv.services.platform": {
    "cecVolumeStep": 3
  }
}
```

</td>
<td>

Int

</td>
<td>


3

</td>
<td>

[TVANDROID-5110](https://st.yandex-team.ru/TVANDROID-5110)
<br><code class="inlined">cecVolumeStep</code>:<br> - Шаг изменения громкости голосом
</td>
</tr>
<tr>
<td>

```json
{
  "com.yandex.tv.services.platform": {
    "isStandbyAllowed": true
  }
}
```

</td>
<td>

Boolean

</td>
<td>


true

</td>
<td>

[TVANDROID-5493](https://st.yandex-team.ru/TVANDROID-5493)

</td>
</tr>

<tr>
<td>

```json
{
  "com.yandex.tv.services": {
    "enabledPromos": [],
    "promoTimeout": 3600000
  }
}
```

</td>
<td>

List<String><br>Long

</td>
<td>


[]<br>3600000

</td>
<td>

[TVANDROID-5179](https://st.yandex-team.ru/TVANDROID-5179)
<br><code class="inlined">enabledPromos</code>:<br> - Включенные промо, для которых будет произведена попытка сходить (на бекенд) за дивной версткой, чтобы отрисовать.<br><code class="inlined">promoTimeout</code>:<br> - Время (количество милисекунд) после показа какого-либо промика, в течение которого не должен быть показан очередной промик
</td>
</tr>

<tr>
<td>

```json
{
  "com.yandex.tv.services": {
    "tandemSetup": {
      "tandemSetupEnabled": false
    }
  }
}
```

</td>
<td>

Boolean

</td>
<td>


BoardUtils.isDeviceStb()

</td>
<td>

[TVANDROID-5123](https://st.yandex-team.ru/TVANDROID-5123)
<br><code class="inlined">tandemSetupEnabled</code>:<br> - Включает экран настройки тандема в суве, значение по-умолчанию – true для модуля, иначе false. Тикет утерян.
</td>
</tr>
<tr>
<td>

```json
{
  "com.yandex.tv.services": {
    "tandemSetup": {
      "backgrounds": "{}"
    }
  }
}
```

</td>
<td>

Object

</td>
<td>


{}

</td>
<td>

[YATV-21](https://st.yandex-team.ru/YATV-21)
<br><code class="inlined">backgrounds</code>:<br> - Настройка бэкграундов для экрана создания тандема в суве. Описание формата и подробности о том, как применяется настройка, в комменте: https://st.yandex-team.ru/YATV-21#6141fdbdbd29ea364553f0b3.
</td>
</tr>
<tr>
<td>

```json
{
  "com.yandex.tv.services": {
    "tandemSetup": {
      "icons": "{}",
      "deviceChoosingEnabled": false
    }
  }
}
```

</td>
<td>

Object<br>Boolean

</td>
<td>


{}<br>false

</td>
<td>

[TVANDROID-5115](https://st.yandex-team.ru/TVANDROID-5115)
<br><code class="inlined">icons</code>:<br> - Иконки для каждого вида моделей и цветов колонок.<br><code class="inlined">deviceChoosingEnabled</code>:<br> - Включает возможность выбора колонок в SUW-е, если их рядом несколько.
</td>
</tr>
<tr>
<td>

```json
{
  "com.yandex.tv.services": {
    "tandemSetup": {
      "searchAppUrl": "https://yandex.ru/quasar/external/open-module-group-settings?moduleId\u003d{{DEVICE_ID}}\u0026modulePlatform\u003d{{PLATFORM}}"
    }
  }
}
```

</td>
<td>

String

</td>
<td>


https://yandex.ru/quasar/external/open-module-group-settings?moduleId={{DEVICE_ID}}&modulePlatform={{PLATFORM}}

</td>
<td>

[TVANDROID-4938](https://st.yandex-team.ru/TVANDROID-4938)
<br><code class="inlined">searchAppUrl</code>:<br> - Заменяет урл, который зашифрован в QR-код на экране создания тандема в суве.
</td>
</tr>
<tr>
<td>

```json
{
  "tandemColorCodesConfig": "{}"
}
```

</td>
<td>

Object

</td>
<td>


{}

</td>
<td>

[TVANDROID-4923](https://st.yandex-team.ru/TVANDROID-4923)
<br><code class="inlined">tandemColorCodesConfig</code>:<br> - В старых доках этого флага нет, но в коде он есть, поэтому вот он.
</td>
</tr>
<tr>
<td>

```json
{
  "com.yandex.tv.services": {
    "tandemSetup": {
      "tandemSuccessUrl": "https://yandex.ru/support/module/tandem.html"
    }
  }
}
```

</td>
<td>

String

</td>
<td>


https://yandex.ru/support/module/tandem.html

</td>
<td>

[TVANDROID-5083](https://st.yandex-team.ru/TVANDROID-5083)
<br><code class="inlined">tandemSuccessUrl</code>:<br> - Ссылка (QR) после успешной настроки.
</td>
</tr>

<tr>
<td>

```json
{
  "com.yandex.tv.services": {
    "accessibilityConfig": {
      "serviceEnabled": false,
      "notificationTimeoutMs": 100,
      "packages": [],
      "unresponsiveUiTimeoutMs": 2000
    }
  }
}
```

</td>
<td>

Boolean<br>Long<br>List<String><br>Long

</td>
<td>


false<br>100<br><br>2000

</td>
<td>

[TVANDROID-5613](https://st.yandex-team.ru/TVANDROID-5613)
<br><code class="inlined">serviceEnabled</code>:<br> - Включает YandexAccessibilityService для конфигурирования параметров из https://developer.android.com/reference/android/accessibilityservice/AccessibilityServiceInfo#xml-attributes_1<br><code class="inlined">unresponsiveUiTimeoutMs</code>:<br> - Через сколько мс после события нажатия должно пройти без изменения ui чтобы отправилось событие tv_ui_unresponsive
</td>
</tr>

<tr>
<td>

```json
{
  "yandexTvGeneral": {
    "mandatoryAuth": false
  },
  "com.yandex.tv.setupwizard": {
    "canSkipSuw": false,
    "isWelcomeScreenTimerEnabled": true,
    "isRetailModeAvailable": false,
    "compatibleRemoteControllers": [],
    "remoteControllerScreen": ""
  },
  "com.yandex.tv.services": {
    "canRemoteControllerMakeSounds": false
  }
}
```

</td>
<td>

Boolean<br>Boolean<br>Boolean<br>Boolean<br>List<String><br>String<br>Boolean

</td>
<td>


false<br>false<br>true<br>false<br><br><br>false

</td>
<td>

[TVANDROID-5701](https://st.yandex-team.ru/TVANDROID-5701)
<br><code class="inlined">mandatoryAuth</code>:<br> - [Зависит от платформы](https://a.yandex-team.ru/arc_vcs/smart_devices/android/tv/services/sdk-iosdk/src/main/assets?rev=r9393152)
</td>
</tr>
<tr>
<td>

```json
{
  "com.yandex.io.sdk": {
    "rawEdidPath": ""
  }
}
```

</td>
<td>

String

</td>
<td>




</td>
<td>

[TVANDROID-5396](https://st.yandex-team.ru/TVANDROID-5396)

</td>
</tr>
<tr>
<td>

```json
{
  "com.yandex.tv.services": {
    "hasYandexRcu": false
  }
}
```

</td>
<td>

Boolean

</td>
<td>


false

</td>
<td>

[ALICE-19299](https://st.yandex-team.ru/ALICE-19299)
<br><code class="inlined">hasYandexRcu</code>:<br> - aka hasOmniRcu. Означает, что устройство использует пульт от Яндекса (OMNI). Подключает сервис с фичами для обновления, настройки, звуков и тд
</td>
</tr>
<tr>
<td>

```json
{
  "com.yandex.tv.setupwizard": {
    "demoModePromotionEnabled": false,
    "packagedRemoteName": "generic"
  }
}
```

</td>
<td>

Boolean<br>String

</td>
<td>


false<br>generic

</td>
<td>

[TVANDROID-6261](https://st.yandex-team.ru/TVANDROID-6261)

</td>
</tr>
<tr>
<td>

```json
{
  "com.yandex.tv.setupwizard": {
    "isStrictUpdaterResultCheck": false
  }
}
```

</td>
<td>

Boolean

</td>
<td>


false

</td>
<td>

[TVANDROID-4567](https://st.yandex-team.ru/TVANDROID-4567)

</td>
</tr>
<tr>
<td>

```json
{
  "com.yandex.tv.setupwizard": {
    "isTimeZoneManagerEnabled": false
  }
}
```

</td>
<td>

Boolean

</td>
<td>


false

</td>
<td>

[TVANDROID-4450](https://st.yandex-team.ru/TVANDROID-4450)

</td>
</tr>
<tr>
<td>

```json
{
  "yandexTvGeneral": {
    "quickPingsEnabled": false
  }
}
```

</td>
<td>

Boolean

</td>
<td>


false

</td>
<td>

[TVANDROID-6389](https://st.yandex-team.ru/TVANDROID-6389)

</td>
</tr>

<tr>
<td>

```json
{
  "com.yandex.tv.videoplayer": {
    "maxHistoryCount": 130
  }
}
```

</td>
<td>

Int

</td>
<td>


130

</td>
<td>

[TVANDROID-6380](https://st.yandex-team.ru/TVANDROID-6380)

</td>
</tr>
<tr>
<td>

```json
{
  "com.yandex.tv.videoplayer": {
    "playerCachedThreadPool": false
  }
}
```

</td>
<td>

Boolean

</td>
<td>


false

</td>
<td>

[TVANDROID-6310](https://st.yandex-team.ru/TVANDROID-6310)

</td>
</tr>

<tr>
<td>

```json
{
  "com.yandex.tv.input.efir": {
    "complete_programs_update_enabled": false
  }
}
```

</td>
<td>

Boolean

</td>
<td>


false

</td>
<td>

[ALICE-14678](https://st.yandex-team.ru/ALICE-14678)

</td>
</tr>
<tr>
<td>

```json
{
  "com.yandex.tv.input.efir": {
    "player_buffer_for_playback_ms": 2500
  }
}
```

</td>
<td>

Int

</td>
<td>


2500

</td>
<td>

[TVANDROID-5281](https://st.yandex-team.ru/TVANDROID-5281)

</td>
</tr>
<tr>
<td>

```json
{
  "com.yandex.tv.input.efir": {
    "smotreshka_channels_enabled": false
  }
}
```

</td>
<td>

Boolean

</td>
<td>


false

</td>
<td>

[TVANDROID-5366](https://st.yandex-team.ru/TVANDROID-5366)

</td>
</tr>
<tr>
<td>

```json
{
  "com.yandex.tv.input.efir": {
    "programsZipInMemory": false
  }
}
```

</td>
<td>

Boolean

</td>
<td>


false

</td>
<td>

[TVANDROID-6381](https://st.yandex-team.ru/TVANDROID-6381)

</td>
</tr>

<tr>
<td>

```json
{
  "com.yandex.tv.live": {
    "channelSwitching": {
      "validateSubscriptionAsyncEnabled": false,
      "subscriptionValidTimeMs": 60000
    }
  }
}
```

</td>
<td>

Boolean<br>Long

</td>
<td>


false<br>60000

</td>
<td>

[TVANDROID-5427](https://st.yandex-team.ru/TVANDROID-5427)

</td>
</tr>
<tr>
<td>

```json
{
  "com.yandex.tv.live": {
    "channelSwitching": {
      "restartInputServiceOnChannelSwitched": true
    }
  }
}
```

</td>
<td>

Boolean

</td>
<td>


true

</td>
<td>

[TVANDROID-5426](https://st.yandex-team.ru/TVANDROID-5426)

</td>
</tr>
<tr>
<td>

```json
{
  "com.yandex.tv.live": {
    "channelThumbStubs": []
  }
}
```

</td>
<td>

List<String>

</td>
<td>




</td>
<td>

[TVANDROID-5423](https://st.yandex-team.ru/TVANDROID-5423)

</td>
</tr>
<tr>
<td>

```json
{
  "com.yandex.tv.live": {
    "paidChannelStubV2Enabled": false
  }
}
```

</td>
<td>

Boolean

</td>
<td>


false

</td>
<td>

[TVANDROID-6098](https://st.yandex-team.ru/TVANDROID-6098)

</td>
</tr>

<tr>
<td>

```json
{
  "com.yandex.tv.videoplayer": {
    "adsEnabledProd": false,
    "adsPageId": "false"
  }
}
```

</td>
<td>

Boolean<br>String

</td>
<td>


false<br>false

</td>
<td>

[TVANDROID-3560](https://st.yandex-team.ru/TVANDROID-3560)
<br><code class="inlined">adsPageId</code>:<br> - Задание рекламного pageId для отладки. <br> В бою - pageId привязан к каждому конкретному видео. Вручную размечают в ВХ.<br>1378525 - реклама с adPod-ами, приходит не гарантированно<br>R-M-DEMO-instream-vmap - реклама без adPod-ов, зато приходит гарантированно
</td>
</tr>


</tbody>
</table>
