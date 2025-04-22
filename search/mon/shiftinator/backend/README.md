копируем и редактируем под себя дев-конфиг, путь к конфигу передается через переменную окружения SHIFT_CONFIG

создаем тестовую базу

psql -d postgres

CREATE USER shiftinator_admin;
CREATE DATABASE shiftinator_test_db OWNER shiftinator_admin;
ALTER USER shiftinator_admin WITH PASSWORD 'password';

export SHIFT_VER=0 && \
docker build -t shiftinator . && \
docker tag shiftinator registry.yandex.net/searchmon/shiftinator:$SHIFT_VER && \
docker push registry.yandex.net/searchmon/shiftinator:$SHIFT_VER

docker run -it --rm -p 8000:8000 -e SHIFTINATOR_CONFIG='/app/config/dev.yaml' --name shiftinator shiftinator bash

ya upload config/config.yaml -T OTHER_RESOURCE --owner bayanist01 --ttl 7 -d 'prod config'
ya upload config/prestable.yaml -T OTHER_RESOURCE --owner bayanist01 --ttl 7 -d 'test config'

pip install tvmtool-bin -i https://pypi.yandex-team.ru/simple

alembic revision --autogenerate

alembic upgrade head
