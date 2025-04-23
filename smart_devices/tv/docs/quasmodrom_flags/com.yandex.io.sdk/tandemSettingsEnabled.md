# tandemSettingsEnabled
**Type:** Object
**Default:** -

**Related tickets**
[TVANDROID-5115](https://st.yandex-team.ru/TVANDROID-5115)

**Context**
```json
{
  "com.yandex.io.sdk": {
    "tandemSettingsEnabled": true
  },
  "com.yandex.tv.services": {
    "tandemSetup": {
      "Key": "\u043f\u0440\u043e\u0434\u0443\u0431\u043b\u0438\u0440\u043e\u0432\u0430\u0442\u044c \u0437\u043d\u0430\u0447\u0435\u043d\u0438\u044f \u0438\u0437 com.yandex.tv.setupwizard \u0432 tandemSetup"
    }
  },
  "com.yandex.tv.setupwizard": {
    "tandemSetup": {
      "deviceChoosingEnabled": true,
      "icons": {
        "yandexstation": {
          "default": {
            "default": "https://androidtvprod.s3.yandex.net/tandem_icons/station_1.png",
            "stereopair": "https://androidtvprod.s3.yandex.net/tandem_icons/station_1_stereo.png"
          }
        },
        "yandexstation_2": {
          "K": {
            "default": "https://androidtvprod.s3.yandex.net/tandem_icons/station_2_black.png",
            "stereopair": "https://androidtvprod.s3.yandex.net/tandem_icons/station_2_black_stereo.png"
          },
          "W": {
            "default": "https://androidtvprod.s3.yandex.net/tandem_icons/station_2_white.png",
            "stereopair": "https://androidtvprod.s3.yandex.net/tandem_icons/station_2_white_stereo.png"
          },
          "B": {
            "default": "https://androidtvprod.s3.yandex.net/tandem_icons/station_2_blue.png",
            "stereopair": "https://androidtvprod.s3.yandex.net/tandem_icons/station_2_blue_stereo.png"
          },
          "R": {
            "default": "https://androidtvprod.s3.yandex.net/tandem_icons/station_2_red.png",
            "stereopair": "https://androidtvprod.s3.yandex.net/tandem_icons/station_2_red_stereo.png"
          },
          "default": {
            "default": "https://androidtvprod.s3.yandex.net/tandem_icons/station_2_black.png",
            "stereopair": "https://androidtvprod.s3.yandex.net/tandem_icons/station_2_black_stereo.png"
          }
        },
        "yandexmini": {
          "default": {
            "default": "https://androidtvprod.s3.yandex.net/tandem_icons/mini_1_black.png",
            "stereopair": "https://androidtvprod.s3.yandex.net/tandem_icons/mini_1_black_stereo.png"
          }
        },
        "yandexmini_2": {
          "K": {
            "default": "https://androidtvprod.s3.yandex.net/tandem_icons/mini_2_black.png",
            "stereopair": "https://androidtvprod.s3.yandex.net/tandem_icons/mini_2_black_stereo.png"
          },
          "G": {
            "default": "https://androidtvprod.s3.yandex.net/tandem_icons/mini_2_gray.png",
            "stereopair": "https://androidtvprod.s3.yandex.net/tandem_icons/mini_2_gray_stereo.png"
          },
          "B": {
            "default": "https://androidtvprod.s3.yandex.net/tandem_icons/mini_2_blue.png",
            "stereopair": "https://androidtvprod.s3.yandex.net/tandem_icons/mini_2_blue_stereo.png"
          },
          "R": {
            "default": "https://androidtvprod.s3.yandex.net/tandem_icons/mini_2_red.png",
            "stereopair": "https://androidtvprod.s3.yandex.net/tandem_icons/mini_2_red_stereo.png"
          },
          "default": {
            "default": "https://androidtvprod.s3.yandex.net/tandem_icons/mini_2_black.png",
            "stereopair": "https://androidtvprod.s3.yandex.net/tandem_icons/mini_2_black_stereo.png"
          }
        },
        "yandexmicro": {
          "G": {
            "default": "https://androidtvprod.s3.yandex.net/tandem_icons/micro_green.png",
            "stereopair": "https://androidtvprod.s3.yandex.net/tandem_icons/micro_green_stereo.png"
          },
          "P": {
            "default": "https://androidtvprod.s3.yandex.net/tandem_icons/micro_purple.png",
            "stereopair": "https://androidtvprod.s3.yandex.net/tandem_icons/micro_purple_stereo.png"
          },
          "R": {
            "default": "https://androidtvprod.s3.yandex.net/tandem_icons/micro_red.png",
            "stereopair": "https://androidtvprod.s3.yandex.net/tandem_icons/micro_red_stereo.png"
          },
          "B": {
            "default": "https://androidtvprod.s3.yandex.net/tandem_icons/micro_beige.png",
            "stereopair": "https://androidtvprod.s3.yandex.net/tandem_icons/micro_beige_stereo.png"
          },
          "Y": {
            "default": "https://androidtvprod.s3.yandex.net/tandem_icons/micro_yellow.png",
            "stereopair": "https://androidtvprod.s3.yandex.net/tandem_icons/micro_yellow_stereo.png"
          },
          "N": {
            "default": "https://androidtvprod.s3.yandex.net/tandem_icons/micro_pink.png",
            "stereopair": "https://androidtvprod.s3.yandex.net/tandem_icons/micro_pink_stereo.png"
          },
          "default": {
            "default": "https://androidtvprod.s3.yandex.net/tandem_icons/micro_green.png",
            "stereopair": "https://androidtvprod.s3.yandex.net/tandem_icons/micro_green_stereo.png"
          }
        },
        "default": "https://androidtvprod.s3.yandex.net/tandem_icons/station_1.png"
      }
    }
  }
}
```

**Description**
`tandemSettingsEnabled ` - Включает управление тандемом через настройки. 
`deviceChoosingEnabled` - Включает возможность выбора колонок в SUW-е, если их рядом несколько.
`icons` - иконки для каждого вида моделей и цветов колонок.

подробнее в 
