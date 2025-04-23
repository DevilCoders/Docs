Тестовые файлы были получены следующим способом.

В функцию `PredictionsStore::findInBBox` была добавлена функция `save` со следущим кодом:
```cpp
void save(const std::vector<PredictionRef>& preds) {
    std::string filename =
        "/logs/yandex/maps/mtinfo/" + std::to_string(std::time(0)) + "_" + std::to_string(preds.size()) + ".pb";
    std::ofstream fout(filename);
    maps::masstransit::ydbfree::predictions_dataset::ForecastsWriter writer{fout};
    for (const auto pref : preds) {
        writer << pref.get();
    }
    INFO() << "@ saved predictions to " << filename;
}
```

Бинарь был scpшнут на mtinfo-load, затем руками открывались тестовые карты с хостом, куда был scpшнут бинарь:
`https://l7test.yandex.ru/maps/?host_config[inthosts][mtinfo]=http://slbvfa75cio7fsks.sas.yp-c.yandex.net/`
Далее в картах открывался нужный bbox, протобуфный файл появлялся на mtinfo и аплоадился в сендбокс.

TODO: способ очень деревянный (хоть и работает), нужно научиться генерировать файл с предсказаниями самому, потому что
при изменении формата протобуфа, действия выше нужно будет проделать заново.
Также путь `/logs/yandex/maps/mtinfo/` подходил, потому что у mtinfo нет прав на записи в другие пути, конечно потом
нужно не забыть удалить предикшены, чтобы не засорять mtinfo-load.
