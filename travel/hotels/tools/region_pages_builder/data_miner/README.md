# City pages data miner

## Build & run

```
 ya make -tt bin && ./bin/region_pages_data_miner --yql-token $(cat ~/.yql/token) --yt-token $(cat ~/.yt/token)
```

## CI configuration

- Sandbox resource: [TRAVEL_HOTELS_REGION_PAGES_DATA_MINER](https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/projects/Travel/resources/__init__.py?rev=7227141#L799)
- Testenv job: [TRAVEL_MAKE_REGION_PAGES_DATA_MINER](https://a.yandex-team.ru/arc/trunk/arcadia/testenv/jobs/travel/TravelBuild.yaml?rev=7257820#L610)

## Tasks in Sandbox

- [TESTING](https://sandbox.yandex-team.ru/tasks?children=true&tags=TYPE%3ATRAVEL_HOTELS_REGION_PAGES_DATA_MINER%2CENV%3ATESTING&all_tags=true&limit=20)
- [PROD](https://sandbox.yandex-team.ru/tasks?children=true&tags=TYPE%3ATRAVEL_HOTELS_REGION_PAGES_DATA_MINER%2CENV%3APROD&all_tags=true&limit=20)
