# BoY patners catroom builder

## Dolphin catroom builder

Builds catroom index from Dolphin search log.

**Run in develop:**

```shell script
ya make . && ./boy_catroom_builder --partner dolphin --yql-token $(cat ~/.yql/token) [--days 1] [--date 2019-12-01]
```

**Run in testing:**

```shell script
ya make . && ./boy_catroom_builder --partner dolphin --yql-token $(cat ~/.yql/token) --base-dir //home/travel/testing/catroom
```

**Run in production:**

```shell script
ya make . && ./boy_catroom_builder --partner dolphin --yql-token <production-token> --base-dir //home/travel/prod/catroom
```

### Hitman 

[Prod](https://hitman.yandex-team.ru/projects/hotels/travel_hotels_tools_boy_catroom_builder_dolphin_prod)

[Test](https://hitman.yandex-team.ru/projects/hotels/travel_hotels_tools_boy_catroom_builder_dolphin_test)

## Expedia catroom builder

Builds catroom index from expedia feed.

**Run in develop:**

```shell script
ya make . && ./boy_catroom_builder --partner expedia --yql-token $(cat ~/.yql/token) [--feed-table //path/to/yt/table]
```

**Run in testing:**

```shell script
ya make . && ./boy_catroom_builder --partner expedia --yql-token $(cat ~/.yql/token) --base-dir //home/travel/testing/catroom [--feed-table //path/to/yt/table]
```

**Run in production:**

```shell script
ya make . && ./boy_catroom_builder --partner expedia --yql-token <production-token> --base-dir //home/travel/prod/catroom
```

### Hitman 

[Prod](https://hitman.yandex-team.ru/projects/hotels/travel_hotels_tools_boy_catroom_builder_expedia_prod)

[Test](https://hitman.yandex-team.ru/projects/hotels/travel_hotels_tools_boy_catroom_builder_expedia_test)

## Travelline catroom builder

Builds catroom index from Travelline feed.

**Run in develop:**

```shell script
ya make . && ./boy_catroom_builder --partner travelline --yql-token $(cat ~/.yql/token) [--feed-table //path/to/yt/table]
```

**Run in testing:**

```shell script
ya make . && ./boy_catroom_builder --partner travelline --yql-token $(cat ~/.yql/token) --base-dir //home/travel/testing/catroom [--feed-table //path/to/yt/table]
```

**Run in production:**

```shell script
ya make . && ./boy_catroom_builder --partner travelline --yql-token <production-token> --base-dir //home/travel/prod/catroom
```

### Hitman 

[Prod](https://hitman.yandex-team.ru/projects/hotels/travel_hotels_tools_boy_catroom_builder_travelline_prod)

[Test](https://hitman.yandex-team.ru/projects/hotels/travel_hotels_tools_boy_catroom_builder_travelline_test)
