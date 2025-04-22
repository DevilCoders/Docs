# screen_height
**Type:** complex
**Default:** -

**Related tickets**
[QUASARINFRA-423](https://st.yandex-team.ru/QUASARINFRA-423)
[TVANDROID-4414](https://st.yandex-team.ru/TVANDROID-4414)
[TVANDROID-4272](https://st.yandex-team.ru/TVANDROID-4272)
[QUASARINFRA-423](https://st.yandex-team.ru/QUASARINFRA-423)

**Context**
```json
{
  "PACKAGE": {
    "media": {
      "TYPE": {
        "MEDIA_KEY": {
          "SIZE_LABEL": {
            "screen_width": "Int",
            "screen_height": "Int",
            "url": "String",
            "file_size": "Int",
            "max_download_time": "Int"
          }
        }
      }
    }
  }
}
```

**Description**
Скачиваемые видео и картинки по всему тв





все параметры обязательные
`Параметр` | `Описание`
:--- | :---
##PACKAGE## | как правило app package в котором файл используется
##MEDIA_TYPE## | ##image## или ##video##
##MEDIA_KEY## | ключ (имя) медиа файла, должен быть говорящим, однозначным
##SIZE_LABEL## | метка для "размеро варианта", дефолтный размер - ##default##, дополнительные метки могут иметь произвольное значения, но обязаны иметь заполненные значения ##screen_width## и/или ##screen_height## в пикселях, подробнее в коментарии: #611149b69f5fd46ae3a7b54e
##screen_width## : value | Int: размер в пикселях, опционально, см описание ##SIZE_LABEL##
##screen_height## : value | Int: размер в пикселях, опционально, см описание ##SIZE_LABEL##
##url## : value | String: https ссылка на ресурс, видео предпочтительно h264, 16:9, картинки jpg\png, смотря куда лучше ложится
##file_size## : value | Int: размер файла в байтах
##max_download_time## : value | Int: максимальное время скачивания, по его истечению клиент прекратит скачивание


Известные Media файлы:
большинство должно быть перечислено здесь:
[https://a.yandex-team.ru/arc_vcs/smart_devices/android/tv/common/media-downloader/src/main/java/com/yandex/tv/common/media/MediaLookups.kt](https://a.yandex-team.ru/arc_vcs/smart_devices/android/tv/common/media-downloader/src/main/java/com/yandex/tv/common/media/MediaLookups.kt)


#|
|| `PACKAGE` | `MEDIA_TYPE` | `MEDIA_KEY` | `Описание` ||
|| ##com.yandex.tv.setupwizard## | ##image## | ##suwAuthPromoBackgroundImage## | фон Auth Promo экрана в suw ||
|| ##com.yandex.tv.setupwizard## | ##image## | ##suwAuthSkipBackgroundImage## | фон Auth Skip экрана в suw ||
|| ##com.yandex.tv.services## | ##image## | ##passportGiftPromoBackgroundImage## | фон экрана Gift Promo в сервисах\паспорте\AuthActivity ||
|| ##com.yandex.tv.services## | ##image## | ##passportGiftCardEntrySideImage## | Боковая картинка на alice gift flow при выборе карты ||
|| ##com.yandex.launcher.updaterapp## | ##video## | ##suwUpdateBackgroundVideo## | фоновое видео экрана загрузки обновлений в Suw ||
|| ##com.yandex.launcher.updaterapp## | ##video## | ##forcedUpdateBackgroundVideo## | фоновое видео экрана загрузки обновлений при показе Forced update ui ||
|#

пример конфига: [https://paste.yandex-team.ru/4966600](https://paste.yandex-team.ru/4966600)
