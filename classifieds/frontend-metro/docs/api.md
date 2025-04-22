# API
* [hasMetro(cityId)](#hasMetro)
* [getStationById(stationId)](#getStationById)
* [getLineById(lineId)](#getLineById)
* [getLinesIdsByCityId(cityId)](#getLinesIdsByCityId)
* [getStationsIdsByLineId(lineId)](#getStationsIdsByLineId)
* [getStationsIdsByCityId(cityId)](#getStationsIdsByCityId)
* [hasRingLine(cityId)](#hasRingLine)

<a name="hasMetro"></a>
### hasMetro(cityId)
**Params**

- cityId `Number` - Идентификатор города

**Returns**: `Boolean` - Флаг наличия в городе метро
<a name="getStationById"></a>
### getStationById(stationId)
**Params**

- stationId `Number` - Идентификатор станции

**Returns**: `?Station` - Информация о станции
<a name="getLineById"></a>
### getLineById(lineId)
**Params**

- lineId `String` - Идентификатор линии метро

**Returns**: `?Line` - Информация о линии
<a name="getLinesIdsByCityId"></a>
###getLinesIdsByCityId(cityId)
**Params**

- cityId `Number` - Идентификатор города

**Returns**: `String[]` - Список идентификаторов линий
<a name="getStationsIdsByLineId"></a>
### getStationsIdsByLineId(lineId)
**Params**

- lineId `String` - Идентификатор линии метро

**Returns**: `Number[]` - Идентификаторы всех станций на этой ветке
<a name="getStationsIdsByCityId"></a>
### getStationsIdsByCityId(cityId)
**Params**

- cityId `Number` - Идентификатор города

**Returns**: `Number[]` - Идентификаторы станций метро в этом городе
<a name="hasRingLine"></a>
### hasRingLine(cityId)
**Params**

- cityId `Number` - Идентификатор города

**Returns**: `Boolean` - Флаг наличия в городе кольцевой линии метрополитена
