Нагрузочное тестирование
========================

Генерируем дефолтные патроны:
`./carter-tank-default.sh > ammo.txt`

Генерируем кастомные патроны: 
`./carter-tank.py min_user_id max_user_id size read_rps write_rps > ammo.txt`

Скрипт сгенерирует `size` запросов к корзинам пользователей с `id` такими, что `min_user_id <= id <= min_user_id` и соотношением `get` к `post` запросам: `read_rps / write_eps`

Подробнее про нагрузочное тестирование наших компонентов [здесь](https://wiki.yandex-team.ru/market/development/pers/load/ "Нагрузочное тестирование бэкэндов PERS")