# Переключение мастера в Greenbox

## Алерты
О неполадках с мастером могут подсказать алерты вида portal.greenbox:topnews_data*_age, например:

[topnews_data_age](https://juggler.yandex-team.ru/project/portal/aggregate?host=portal.greenbox&service=topnews_data_age&project=portal)
[topnews_new_data_age](https://juggler.yandex-team.ru/project/portal/aggregate?host=portal.greenbox&service=topnews_new_data_age&project=portal)

## Где посмотреть состояние кластера
Данные сервиса greenbox живут в [redis кластере MDB](https://cloud.yandex-team.ru/folders/foocqso83qg8i157m8tr/managed-redis/cluster/mdbpceivm7uenj2nsk6a?section=overview).

Чтобы проверить состояние мастера проделайте следующие шаги:
1. Откройте [панель управления redis кластером](https://cloud.yandex-team.ru/folders/foocqso83qg8i157m8tr/managed-redis/cluster/mdbpceivm7uenj2nsk6a?section=overview).
1. Перейдите на вкладку "Хосты".
2. Убедитесь, что в данный момент времени есть хост в состоянии "ALIVE" и ролью "MASTER".

![](https://jing.yandex-team.ru/files/cheetah/2022-05-16T09%3A51%3A51Z.03bf001.png =x400){: .center}

## Если что-то пошло не так {when-something-goes-wrong}
1. Промотрите основные чаты Морда (факапочная) и Координация Большах Факапов (КБФ) на предмет поломок ДЦ.
2. Определите время ETA до восстановления работоспособности прода.
3. Согласуйте риски с менеджером Сергей Байбик baibik@.
4. При необходимости попросите в MDB Emergency переключить мастера на оставшийся хост.

Если по каким-то причинам возникают сложности в пунктами 1-3, тогда сразу приступайте к пункту 4.
