## О компоненте
Сервис для поставки данных по партнеру для поиска в партнерском интерфейсе.
Читает данные из очереди в LB и из YT, сохраняет состояние партнера и пушит данные в elasticsearch

## Релизная машина в TSUM
[Релизная машина](https://tsum.yandex-team.ru/pipe/projects/mbi/delivery-dashboard/mbi-partner-search)

## Сборка и тестирование
[ya.make](https://wiki.yandex-team.ru/yatool/make/)
cd ~/arc/arcadia; ./ya ide idea --iml-in-project-root -lr ~/projects/IdeaProjects/mbi-partner-search market/mbi/mbi-partner-search
