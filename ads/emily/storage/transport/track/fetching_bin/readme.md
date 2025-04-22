# Delivery Tracking Fetchers

## Интерфейс

Интерфейс лежит [тут](https://a.yandex-team.ru/arc_vcs/ads/emily/storage/transport/track/fetching_bin/lib/fetchers/base/fetcher_base.py#L8).

У интерфейса один метод **get_info**, который вызывается для каждого key, version модели из конфига и должен вернуть [**FetchedModelInfo**](https://a.yandex-team.ru/arc_vcs/ads/emily/storage/transport/track/fetching_bin/lib/fetchers/base/fetched_model_info.py#L6).

## FetchedModelInfo

[**FetchedModelInfo**](https://a.yandex-team.ru/arc_vcs/ads/emily/storage/transport/track/fetching_bin/lib/fetchers/base/fetched_model_info.py#L6) – класc, который хранит необходимую информацию для трекинга: key, version модели, а также TModelStates (который пока просто словарь, имеющий следующий [формат](https://st.yandex-team.ru/EMILY-356#6266d5211864952e2194136b))

## Реализация

Для реализации своего фетчера необходимо проделать следующее:

1. Реализовать свой фетчер, отнаследовавшись от [**IFetcher**](https://a.yandex-team.ru/arc_vcs/ads/emily/storage/transport/track/fetching_bin/lib/fetchers/base/fetcher_base.py#L8).
2. Дополнить [**enum**](https://a.yandex-team.ru/arc_vcs/ads/emily/storage/transport/track/fetching_bin/__main__.py#L23) новым типом фетчера.
3. Добавить правило конструирование нового фетчера в [**фабрику**](https://a.yandex-team.ru/arc_vcs/ads/emily/storage/transport/track/fetching_bin/__main__.py#L34)

## Шедулер

[Шедулер](https://sandbox.yandex-team.ru/scheduler/710783/view) запускаются по крону раз в 5 минут.

Используется последний бинарь загруженный на Sandbox.

### Обновить бинарь на Sandbox

```bash
make upload
```