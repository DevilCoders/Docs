В связи с [отключением синка внешнего npm c внутренним](https://clubs.at.yandex-team.ru/devtools-frontend/502/) установить пакеты, которые не были в кеше невозможно (и не секурно).
Как ~~временный костыль (нужна уже папка kostyli)~~ workaround просто подкладываем исходник нужного плагина к себе.

Используем плагин https://github.com/markshapiro/webpack-merge-and-include-globally (как самый простой по объему кода и минимально достаточный для наших нужд). Описание и доку брать из [исходника пакета](https://github.com/markshapiro/webpack-merge-and-include-globally/blob/master/README.md)