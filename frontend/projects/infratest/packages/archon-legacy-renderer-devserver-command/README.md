# archon-legacy-renderer-devserver-command

## Archon-команда `kotik`
Реализует разработческий dev-сервер: запускает и kotik, и templar.
Наследует команду `kotik` из `archon-renderer-devserver-command` и добавляет инициализацию компонента `templar`.
Команда нужна только для миграции старых проектов на новый стек. 

## Archon-компонент `templar`
Поднимает http сервер `templar` на случайном порту.
 
## Middleware `templar-proxy` 
Middleware для `kotik`, которая проксирует запросы в `templar`. 
