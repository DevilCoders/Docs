# Сущность `city`

## `fetchCity`

```typescript
fetchCity: <CityType = City>(request: CityRequest) => Promise<CityResponse<CityType>>;
```

Получает данные про город. Используется на экране профиля для получения
города пользователя.

## `fetchCities`

```typescript
fetchCities: <CityType = City>(request: SearchRequest) => Promise<CitiesResponse<CityType>>;
```

Получает список городов по поисковому запросу.
Учитывает `globalFilters` и `search`.
Может поддерживать пагинацию.
Используется на экране профиля и товара при выборе города пользователя.

## `findCityByCoordinates`

```typescript
findCityByCoordinates?: <CityType = City>(request: CityByCoordinatesRequest) => Promise<CityResponse<CityType>>;
```

Получает ближайший город по координатам, переданным в запросе.
Используя этот метод, приложение может определить, в каком городе находится сейчас пользователь.
