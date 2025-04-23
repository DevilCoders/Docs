# Changelog
All notable changes to this project will be documented in this file.

## [5.1.0]
### Minor non-breaking changes
- Тип `Point` теперь поддерживает третий элемент — высоту.
- Добавлены типы `Span` и `Direction`.

## [5.0.0]
### Breaking Changes
- pixelsBoundsToGeoBounds - ранее мы могли менять местами точки и их координаты в целях нормализации, теперь этого не делаем, так как это приводило к багам (https://st.yandex-team.ru/MAPSUI-21564)

## [4.0.0]
### Breaking Changes
- pixelsToGeo - параметр spherical больше не поддерживается, вместо него третий параметр normalizeLongitude (по-умолчанию, `true`) для возможности отключения нормализации долготы

## [3.1.0]
### Minor non-breaking changes
- findPointProjectionOnLine - появился параметр, который позволит возвращать индекс сегмента при проекции точки на линию.

## [3.0.0]
### Breaking Changes
- create-geodesic-line, solve-direct-problem, solve-inverse-problem: перепортировал либу с 2.1 и заменил Vector на Point.


## [2.0.0]
### Breaking Changes
- Экспортируемые методы разложены каждый в свой файл в одну из тематических папок (pixels, math, geo).
- Добавлены методы геодезии.
- convertBoundsToCenterAndSpan -> boundsToCenterAndSpan.
- boundsFromCenterAndSpan -> centerAndSpanToBounds.
- roundGlobalPixelBounds -> roundGlobalBounds.


## [1.0.0]
### Breaking Changes
- Теперь методы импортятся напрямую из библиотеки.
- point.isEqual -> arePointsEqual
- point.toString -> pointToString
- point.parse -> stringToPoint
- bounds.containsPoint -> boundsContainsPoint
- Проекты, поддерживающие es-модули могут импортировать функции из 'yandex-geo-utils/es' для уменьшения бандла.

#### Пример миграции:
Было:
```
import yandexGeoUtils from 'yandex-geo-utils';

yandexGeoUtils.point.parse(point);
```

Стало:

```
import {stringToPoint} from 'yandex-geo-utils';

stringToPoint(point);
```
