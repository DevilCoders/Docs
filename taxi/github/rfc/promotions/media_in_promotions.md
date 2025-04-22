# Хранение fullscreen в БД
Для хранения в БД используется одна структура fullscreen которая описывает
поля всех существующих коммуникаций.

В этом RFC нас интересует момент связанный с хранением медиа: картинки, видео, анимации (json)
и хранение дополнительной информации о воспроизведении этого медиа.

```python
{
  "id": "5cc0e8eb0c69ff1a8a364b39",
  "created_at": "2019-05-13T21:00:00.0000Z",
  "updated_at": "2019-05-13T21:00:00.0000Z",
  "published_at": "2019-05-13T21:00:00.0000Z",
  "is_published": False,
  "screen": "lavka",
  "start_date": "2019-05-13T21:00:00.0000Z",
  "end_date": "2019-06-30T20:59:00.0000Z",
  "name": "New promo story",
  "promotion_type": "story",
  "priority": 1,
  "meta_tags": [],
  "extra_fields": {
    "preview": {  # структура превьюшки сториза
      "backgrounds": [
        {
          "type": "color",
          "content": "FFFFFF"
        },
        {
          "type": "image",
          "content": "<url>"
        }
      ],
      "main_view": {
        "type": "image",
        "content": "<url>"
      },
    }
  }
  "pages": [
    {
      "icon": "<media_tag_id>",
      "image": "<media_tag_id>",
      "backgrounds": [
        "<media_tag_id>",
        "<media_tag_id>",
        {
          "type": "animation",
          "content":  "url",
          "loop": False
        },
        {
          "type": "color",
          "content": "FFFFFF"
        }
      ],
      "main_view": {  # необязательное поле — описывает основную структуру картинки/анимации
        "type": "image | animation",
        "content": "url",
        "loop": True
      },
    }
  ]
}
```

## С какой проблемой столкнулись
В разных местах коммуникации используются разные способы хранения медиа
Где-то мы отдаем по url, где-то по media_tag а где-то вообще данные хранятся в
самой в строке (color)

Хотелось бы унифицировать способы хранения медиа из различных источников
чтобы можно было одновременно работать с разными источниками и
безболезненно добавлять новые источники

## Предлагаемое решение
Вариант хранения структуры с медиа, на примере backgrounds
потому как в нем и начинается все разнообразие медиа
```python
{
  "backgrounds": [
    {
      "type": "image",
      "content": {
        "stored_as": "media_tag",
        "id": "<media-tag-id>"
        "data": {
          "id": "media_tag_id",
          "type": "image", # duplicate (not necessary)
          "resize_mode": "width_height",
          "sizes": {
            {"field": "height", "value": 640, "mds_id": "<mds-id>", "url": "<url>"},
            {"field": "height", "value": 720, "mds_id": "<mds-id>", "url": "<url>"},
            {"field": "height", "value": 1080 ,"mds_id": "<mds-id>", "url": "<url>"},
          } # "data" не хранится в таблице promotions, если это не string
        }
      },
    },
    {
      "type": "animation",
      "content": {
        "stored_as": "mds",
        "id": "<mds-id>"
        "data": "<url>"
      },
      "loop": True
    },
    {
      "type": "video",
      "content": {
        "stored_as": "media_tag",
        "id": "<media-tag-id>"
        "data": {
          "id": "media_tag_id",
          "type": "image", # duplicate (not necessary)
          "resize_mode": "width_height",
          "sizes": {
            {"field": "height", "value": 640,"mds_id": "<mds-id>", "url": "<url>"},
            {"field": "height", "value": 720,"mds_id": "<mds-id>", "url": "<url>"},
            {"field": "height", "value": 1080,"mds_id": "<mds-id>", "url": "<url>"},
          }
        }
      },
    },
    {
      "type": "color",
      "content": {
        "stored_as": "string",
        "data": "<color-hex>"
      },
    }
  ]
}
```

## Какие футуристичыне сценарии покрывает этот способ хранения
```python
{
  "backgrounds": [
    {
      "type": "image",
      "content": {
        "stored_as": "avatar",
        "namespace": "<avatar-namespace>",
        "id": "<avatar-id>",
        # data сейчас не понятно что здесь будет
      },
    },
    {
      "type": "image",
      "content": {
        "stored_as": "mds",
        "bucket": "<s3-bucket-name>",
        "id": "<mds-id>",
        "data": "<url>",
      },
    },
  ]
}
```


## Как будем переходить на новую структуру
Описанные преобразования применимы ко всем местам, где используются
картинки, видео и иже с ними.
```python
# структура type-content (до)
{
  "type": "video",
  "content": "http://mds.net/some_mds_id",
  "loop": True
}
# (после)
{
  "type": "video",
  "content": {
    "stored_as": "mds",
    "id": "some_mds_id", # будет взят парсингом урла из content
    "data": "http://mds.net/some_mds_id" # не храним базе только для отдачи
  },
  "loop": True
}
```

```python
# media_tag (до)
"<media_tag_id>"

# (после)
{
  "type": "image", # type взятый из media_tag
  "content": {
    "stored_as": "media_tag",
    "id": "<media_tag_id>", # будет взят парсингом урла из content
    "data":  { # не храним базе только для отдачи
      # "id": "media_tag_id", # эти поля будем опускать при отдаче
      # "type": "image",      # так как они бесполезно дублируются
      "resize_mode": "width_height",
      "sizes": {
        {"field": "height", "value": 640, "mds_id": "<mds-id>", "url": "<url>"},
        {"field": "height", "value": 720, "mds_id": "<mds-id>", "url": "<url>"},
        {"field": "height", "value": 1080 ,"mds_id": "<mds-id>", "url": "<url>"},
      }
    }
  },
  "loop": True
}
```