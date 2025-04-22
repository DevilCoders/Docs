# video-client - клиент к ручке метаданных Яндекс.Видео

### Основные функции
getMeta - по URL видео возвращает его метаинформацию из индекса Яндекс.Видео, или null, если информация в индексе не найдена

### Владелец
Группа разработки API к Директу

### Hostname запроса
https://hamster.yandex.ru/video/search

### Пример запроса
https://hamster.yandex.ru/video/search?text=url%3Ahttps%3A%2F%2Fwww.youtube.com%2Fwatch%3Fv%3D0hCBBnZI2AU&json_dump=searchdata.clips.0

### Пример ответа
```json
{
  "searchdata.clips.0": {
    "BanDescription": null,
    "Host": "youtube.com",
    "HtmlAutoplayVideoPlayer": "<iframe src=\"//www.youtube.com/embed/0hCBBnZI2AU?autoplay=1&amp;enablejsapi=1&amp;wmode=opaque\" frameborder=\"0\" scrolling=\"no\" allowfullscreen=\"1\" allow=\"autoplay; fullscreen\" aria-label=\"Video\"></iframe>",
    "HtmlVideoPlayer": "<iframe src=\"//www.youtube.com/embed/0hCBBnZI2AU?enablejsapi=1&amp;wmode=opaque\" frameborder=\"0\" scrolling=\"no\" allowfullscreen=\"1\" allow=\"autoplay; fullscreen\" aria-label=\"Video\"></iframe>",
    "IsPornoDoc": null,
    "PlayerId": "youtube",
    "PlayerParams": {
      "PlayerId": "youtube",
      "PlayerParams": [
        {
          "Name": "id",
          "Value": "0hCBBnZI2AU"
        }
      ]
    },
    "RTBF": null,
    "UgcScenario": null,
    "VideoObjects": null,
    "VisibleHost": "youtube.com",
    "VisibleURL": "http://www.youtube.com/watch?v=0hCBBnZI2AU",
    "VoiceoverLang": null,
    "VoiceoverStudio": null,
    "_factors": null,
    "_markers": [
      "vsnippetizer",
      "RandomLog=eyJUaXRsZSI6IkJNVyBNNSBGOTAgdnMgTUIgRTYzcyDQntCx0LfQvtGAIE1vc2NvdyBMaW1tYSIsIklzUG9ybm9Eb2MiOmZhbHNlLCJBbGxGYWN0b3JzQ3JhdGUiOiJBV2NBQUFCaGJHeGJNRHMzTnpJcElIWnBaR1Z2WDNCeWIyUjFZM1JwYjI1Yk1EczNNVFVwSUhacFpHVnZYM0JsY25OYk56RTFPemMxTVNrZ2RtbGtaVzlmWlhod1pYSnBiV1Z1ZEdGc1d6YzFNVHMzTmpNcElIWnBaR1Z2WDJaeVpYTm9XemMyTXpzM056SXBLd01BQUZBWUVCNDMyYmJhek16OFwvejhBQUlEXC92enY2NzI4ekVCQVFnRElVRkpUUWFXT1wvXC9cLzNcL1VSdkdcL3o3NTlmVVh3YjE5UG5mUG1nQUFnSVFjOGV1cm1IMTl2elwvTnljbFRHaHJhUURZMlwvN3Q3XC9cL2NhQ3d2N0h3UUNndEc4dlB6MTlmMXZBZ0FDQWlCNmNcL01cLzR0ZFhcL1wvXC9cL1dETXprMWhZK1A5MFoyY0Rpb25KU2tvS3pzckthaTR1cmxCS1NpUVdGbVlwS2VsbktTa0o4ZTN0djNSNGVsVjVlSGl3cUtpXC9ob0tDcURnNE9HOXRiVlVlSHA2UmtCRFV4OGVyc2JDd1wvNzlUbFVIOEgwQStcL25ITnpCejM3R3hoVlZWVkhCeU02dWhvbEllSFUzRndzRk1jSEJ5WGpBenh1cnFjdWJpNHpNVEVBSTJNbk9iazVBZUppRWhuWm1ieHU3dGgzdDFsSWlJQ3JwbVpJQkVSdWFxcUNoSVJFZjMzTjZ5Ym0zODZNek1EeU1kbktpb0tLeWtwU1M0dTduOVB4aEhNUHpnMHRKK0ppQWhNUkVTZ016TVRWMVZWNmN6TUpINTNOMGhFUkZ3ek00VlZWYVV6TTdNbUlpSTZuWm1adWFxcVNtZG1aazFFUk1RMU0xTllWVlVNM3QxeHpjeWtNek56d3FvaTkzOTNkM2QzZDNkM2QzZDNkM2QzZFwvXC9cL1wvejl1V1ZsQ0tTbmhrWkJBZVhoNGtvdUxWM2w0T0JVR0J0Sk1URXhTUzB2ejFOUVVyNlFrWWx0YlV4a1ptY2pHeGtRMk5pYkF2elwvOStmbnB6OFwvUFhsNWU1dUxpTWhNVEV4QU9EbWhrWkJBSUNQMGYxOHpNSjNUYTJNWHY3bVlpSWdLdW1aa2dFUkZaU1VrNVB6WFo4MU9UXC9lZW5KanM5TmRuelU1UDlBQUFBQUFBQURBQUF3SGYzcStjcSt6K2RtWm5GNys1T2VIZjNcL1wvOVhjWEN3XC8wOXViZTNlYXdpQ0FGdVdaWW5idGczSWNSd0FBTURcL1wvNWVCZ0FEOVwvXC9cL3VcL3ZcL1wvXC9cLys1N0RIOVwvXC85XC9KQUFBTU5yVUdLVHVCYnZabE9vVW9Vb1QyZ3ZKSSs0b0FRQWdSUldqSUJaSVAxVUREM1M3VUVjeW9iMmErSWljQUpnb3J5RUEySklrU1ozXC9JeFhLXC9aUzZvZ2tBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFMQ1ptWW5OekV4c1ptWmlNek1UUDFWVithbXFDZ0FBZ0orcXFteG1aZ29BQUFBQUFBQUFBQUFBQUFBSEFBQUFBQUJnQUFBQUFBQUFcL3RcLzhcL1wvOG5CZ0FBQUFBQUFBQT0ifQ=="
    ],
    "ads": null,
    "ans_type": "video",
    "authorid": "d3d3LnlvdXR1YmUuY29tO1VDUnlxYzIteGNCSk54YzJIVnQyM3p5dw==",
    "authorname": null,
    "basehost": "sas2-0871.search.yandex.net:28800",
    "category": null,
    "cdt": "2018-06-16T07:00:00+0000",
    "clear_title": "BMW M5 F90 vs MB E63s Обзор Moscow Limma",
    "clip_host": "www.youtube.com",
    "clip_href": "http://www.youtube.com/watch?v=0hCBBnZI2AU",
    "collections_favorites": null,
    "crc": "916074185613833438",
    "detail_url": "/video/search?json_dump=searchdata.clips.0&filmId=13799516566187263301&text=url%3Ahttps%3A%2F%2Fwww.youtube.com%2Fwatch%3Fv%3D0hCBBnZI2AU",
    "docid": "35-16-17-Z56B39EB0ACF0E6E4",
    "dur": "1599",
    "duration": 1599,
    "embed": "y",
    "emoji": "NONE",
    "episode": null,
    "episode_query": null,
    "extra": {
      "related": {
        "no_cnt": 1,
        "parent-reqid": "1552995582813384-1559348227657667002015529-man1-4521-V",
        "related": "{\"rvb\":\"Cs8BCIvlehAAGAAgCCgGMA04C0ACSAlQCFgFYAhofXAOePDqktkFgAG_DIgBuqWfpA6SAQVydXc3MZoBD0dlby9Mb2NhbGl0eUBvbsoBCkkhqtE1lTuW_h_SARRPRAYJ2jlL4jButS87IXAScZUAS9oBDxRuIrtKVt7-zWJtJy7U3OABHugBW_ABOvgBDYACB40CzcxsP5AC6erQ8gGYAgCqAhS9yKVE1fcdfO_wpBCI2WAs_q3IkbICFL3IpUTV9x187_CkEIjZYCz-rciRwAIAEhIKEDQzMjAyODEzNzIzODE4ODIaGAoQNDMyMDI4MTM3MjM4MTg4MhD_ARj_AQ,,\",\"src\":\"serp\",\"url\":\"http://www.youtube.com/watch?v=0hCBBnZI2AU\",\"porno\":null,\"vfp\":1}",
        "relatedVideo": "yes",
        "related_porno": null,
        "related_src": "serp",
        "related_url": "http://www.youtube.com/watch?v=0hCBBnZI2AU",
        "related_vfp": 1,
        "text": "BMW M5 F90 vs MB E63s Обзор Moscow Limma"
      },
      "related_info": {
        "porno": null,
        "rvb": "Cs8BCIvlehAAGAAgCCgGMA04C0ACSAlQCFgFYAhofXAOePDqktkFgAG_DIgBuqWfpA6SAQVydXc3MZoBD0dlby9Mb2NhbGl0eUBvbsoBCkkhqtE1lTuW_h_SARRPRAYJ2jlL4jButS87IXAScZUAS9oBDxRuIrtKVt7-zWJtJy7U3OABHugBW_ABOvgBDYACB40CzcxsP5AC6erQ8gGYAgCqAhS9yKVE1fcdfO_wpBCI2WAs_q3IkbICFL3IpUTV9x187_CkEIjZYCz-rciRwAIAEhIKEDQzMjAyODEzNzIzODE4ODIaGAoQNDMyMDI4MTM3MjM4MTg4MhD_ARj_AQ,,",
        "src": "serp",
        "url": "http://www.youtube.com/watch?v=0hCBBnZI2AU",
        "vfp": 1
      }
    },
    "factors": {
      "IsPornoDoc": null
    },
    "frames": {
      "thumbs": [
        {
          "timestamp": 180,
          "url": "//avatars.mds.yandex.net/get-video_frame/1543486/e354bc1b508d3c7c05ce3ce960cc3336/"
        },
        {
          "timestamp": 420,
          "url": "//avatars.mds.yandex.net/get-video_frame/1666395/9823690d428133c6080607228428759f/"
        },
        {
          "timestamp": 660,
          "url": "//avatars.mds.yandex.net/get-video_frame/1640430/1b6fb58438cd8820c5341e5f69cbc687/"
        },
        {
          "timestamp": 900,
          "url": "//avatars.mds.yandex.net/get-video_frame/1618498/216c96454889d4852ab82b41707066b8/"
        },
        {
          "timestamp": 1140,
          "url": "//avatars.mds.yandex.net/get-video_frame/1513609/4eb010747bb7db0ac9e7e92eb09d1522/"
        },
        {
          "timestamp": 1380,
          "url": "//avatars.mds.yandex.net/get-video_frame/1625143/edfbf7c091cb141216b6f1da58bd2152/"
        },
        {
          "timestamp": 1620,
          "url": "//avatars.mds.yandex.net/get-video_frame/1683970/11efb196074860ec82606b3f6d62ae26/"
        },
        {
          "timestamp": 1860,
          "url": "//avatars.mds.yandex.net/get-video_frame/1527135/6e652cf24c4f8de8a9c9e82348d40a62/"
        },
        {
          "timestamp": 2100,
          "url": "//avatars.mds.yandex.net/get-video_frame/1550652/1e1e2dc86bea088faa45470c82bf8884/"
        },
        {
          "timestamp": 2340,
          "url": "//avatars.mds.yandex.net/get-video_frame/1471688/19bf11d8f9dda0b510d63607a0aec2a8/"
        },
        {
          "timestamp": 2580,
          "url": "//avatars.mds.yandex.net/get-video_frame/1072477/de3553a1e33fdc1c7d6eb6caa9e3bf64/"
        },
        {
          "timestamp": 2820,
          "url": "//avatars.mds.yandex.net/get-video_frame/1664209/5bd1866044e8e737fa467decbbf69db1/"
        },
        {
          "timestamp": 3060,
          "url": "//avatars.mds.yandex.net/get-video_frame/1657226/0057a7ea7d4fa4d0e47acfa87815e246/"
        },
        {
          "timestamp": 3300,
          "url": "//avatars.mds.yandex.net/get-video_frame/1533977/b54fa3a84af8fe86791839cad09f797c/"
        },
        {
          "timestamp": 3540,
          "url": "//avatars.mds.yandex.net/get-video_frame/1550652/49046a273cd79b58cd916c67c7ae561e/"
        }
      ]
    },
    "global_img_id": "1fa3f319a9688257ef22f6c2a2c9da91",
    "green_host": "youtube.com",
    "group_id": "0",
    "group_name": "4320281372381882",
    "group_relevance": "102661160",
    "group_size": 1,
    "hst": "www.youtube.com",
    "html5": "y",
    "html_href": "http://www.youtube.com/watch?v=0hCBBnZI2AU",
    "img_h": "720",
    "img_href": "http://i.ytimg.com/vi/0hCBBnZI2AU/0.jpg",
    "img_w": "1280",
    "is_avod": null,
    "is_new24": "",
    "is_svod": null,
    "is_vdv": null,
    "metahosts": [
      "man1-5451.search.yandex.net:24153",
      "man1-1192.search.yandex.net:8156",
      "man1-4521.search.yandex.net:31250"
    ],
    "middle_color": "726c5f",
    "mtime": "2018-06-16T10:00:00+0300",
    "nid": "1fa3f319a9688257ef22f6c2a2c9da91-00-96",
    "onecolor": null,
    "online": "0",
    "pass": "",
    "players": {
      "autoplay": {
        "html": "<iframe src=\"//www.youtube.com/embed/0hCBBnZI2AU?autoplay=1&amp;enablejsapi=1&amp;wmode=opaque\" frameborder=\"0\" scrolling=\"no\" allowfullscreen=\"1\" allow=\"autoplay; fullscreen\" aria-label=\"Video\"></iframe>"
      },
      "noautoplay": {
        "html": "<iframe src=\"//www.youtube.com/embed/0hCBBnZI2AU?enablejsapi=1&amp;wmode=opaque\" frameborder=\"0\" scrolling=\"no\" allowfullscreen=\"1\" allow=\"autoplay; fullscreen\" aria-label=\"Video\"></iframe>"
      }
    },
    "previews": [
      {
        "height": 1,
        "type": "video/mp4",
        "url": "https://video-preview.s3.yandex.net/12hlIQAAAAA.mp4"
      }
    ],
    "rating": null,
    "raw_pass": "",
    "raw_title": "BMW M5 F90 vs MB E63s Обзор Moscow Limma",
    "relevance": 102661160,
    "rvb": "Cs8BCIvlehAAGAAgCCgGMA04C0ACSAlQCFgFYAhofXAOePDqktkFgAG_DIgBuqWfpA6SAQVydXc3MZoBD0dlby9Mb2NhbGl0eUBvbsoBCkkhqtE1lTuW_h_SARRPRAYJ2jlL4jButS87IXAScZUAS9oBDxRuIrtKVt7-zWJtJy7U3OABHugBW_ABOvgBDYACB40CzcxsP5AC6erQ8gGYAgCqAhS9yKVE1fcdfO_wpBCI2WAs_q3IkbICFL3IpUTV9x187_CkEIjZYCz-rciRwAIAEhIKEDQzMjAyODEzNzIzODE4ODIaGAoQNDMyMDI4MTM3MjM4MTg4MhD_ARj_AQ,,",
    "rvq": "BMW M5 F90 vs MB E63s Обзор Moscow Limma",
    "rvq_query": null,
    "rvq_query_exp": null,
    "search_info": null,
    "season": null,
    "serial": null,
    "sertitle": null,
    "server_descr": "VIDEO",
    "src": "serp",
    "taas": "",
    "tasix": null,
    "thmb_h": "68",
    "thmb_h_orig": 720,
    "thmb_href": "//avatars.mds.yandex.net/get-vthumb/892163/1fa3f319a9688257ef22f6c2a2c9da91",
    "thmb_w": 120,
    "thmb_w_orig": 1280,
    "thumb": "i.ytimg.com/vi/0hCBBnZI2AU/0.jpg",
    "thumbs": {
      "large": {
        "h": 180,
        "url": "//avatars.mds.yandex.net/get-vthumb/892163/1fa3f319a9688257ef22f6c2a2c9da91",
        "w": 320
      },
      "regular": {
        "h": "68",
        "url": "//avatars.mds.yandex.net/get-vthumb/892163/1fa3f319a9688257ef22f6c2a2c9da91",
        "w": 120
      }
    },
    "title": "BMW M5 F90 vs MB E63s Обзор Moscow Limma",
    "url": "http://www.youtube.com/watch?v=0hCBBnZI2AU",
    "v1080hd": "1",
    "valt": null,
    "vc": null,
    "vcclickpixel": null,
    "vcshowpixel": null,
    "vdeephd": null,
    "vdv_progress": null,
    "vhd": "4",
    "vhdbin": "1",
    "videoid": "13799516566187263301",
    "views": "480912",
    "vmusicalbtitle": null,
    "vmusicalbumid": null,
    "vmusicalbyear": null,
    "vmusicartist": null,
    "vmusicartistid": null,
    "vmusiclyrartist": null,
    "vmusiclyrauthor": null,
    "vmusiclyrics": null,
    "vmusiclyrtrack": null,
    "vmusiclyrurls": [],
    "vmusictrack": null,
    "vmusictrackid": null,
    "vtags": null,
    "vthumb_src": "vthumb",
    "vtop": null
  }
}

```

