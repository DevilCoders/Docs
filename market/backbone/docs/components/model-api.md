[ModelApi](https://wiki.yandex-team.ru/market/development/architecture/backbone/model-api)

# Что это?
Архитектура сервиса ModelApi.
Ответственность сервиса: возвращать модельные/мску атрибуты (картинки, тайтл, параметры и их значения), список мску по модели

# ТТХ
Моделей/мску в секунду: ~25к (декстоп+тач) + 3.4к (мобилка) = 28к
Из расчета 100 мску на 1 выдаче.

# Api
Также включает в себя ((/market/development/architecture/backbone/param-api ParamApi))

## POST /v1/models
Возвращает статические атрибуты для модели (не включая мскушных)
**Запрос**
%%(yaml)
- models:
  id: str
%%

**Ответ**
%%(yaml)
- models:
  id: str
  title: str
  - params:
    id: str
    value:
      [oneof]
      id: str
      payload: str
  - pictures:
    width: int
    height: int
    mds:
      group_id: int
      key: str

picture:
  - mds:
    namespace: str
    - thumbs:
      name: str
      width: int
      height: int
%%


# =POST /v1/models/msku-list
Возвращает список msku для модели
**Запрос**
%%(yaml)
- models:
  id: str
%%

**Ответ**
%%(yaml)
- models:
  id: str
  mskus:
    id: str
%%

# =POST /v1/mskus
Возвращает статические атрибуты для msku
**Запрос**
%%(yaml)
- mskus:
  id: str
%%

**Ответ**
%%(yaml)
- mskus:
  id: str
  title: str
  - params:
    id: str
    value:
      [oneof]
      id: str
      payload: str
  - pictures:
    width: int
    height: int
    mds:
      group_id: int
      key: str

picture:
  - mds:
    namespace: str
    - thumbs:
      name: str
      width: int
      height: int
%%

