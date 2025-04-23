# Базовые докер-образы Расписаний

## Перед началом работы

Перед началом работы имеет смысл почитать:

  * https://wiki.yandex-team.ru/qloud/doc/
  * https://docs.docker.com/


## Сборка образов
Автоматическая сборка настроена через TestEnv здесь: 
- https://a.yandex-team.ru/arc/trunk/arcadia/testenv/jobs/rasp/BuildDockerImages.yaml
- https://beta-testenv.yandex-team.ru/project/rasp_tests/timeline

## Базовый образ registry.yandex.net/rasp/ubuntu/trusty

(За основу взят образ Avia https://github.yandex-team.ru/avia/qloud-docker-base)

**Запуск приложения**
Все приложения запускаются через supervisor. Необходимо положить supervisor конфиг, запускающий приложение в `/etc/supervisor/conf.d/`
Приложение может слушать на каком то порту или быть за nginx.
В первом случае - следует использовать порт, указанный в `QLOUD_HTTP_PORT`. Например так:
```
[program:app]
directory = /app
command = gunicorn
    --bind=[::]:%(ENV_QLOUD_HTTP_PORT)s
    --workers=5
    --timeout=30
    --log-level=info
    --access-logfile=/dev/stdout
    --error-logfile=/dev/stderr
    --max-requests=10000
    wsgi
```
Во втором следует положить конфиг nginx в `/etc/nginx/sites-enabled/` и сделать в нем include listen, так как в listen
определяется - на каких портах слушает nginx.

**pre start хуки**
В случае если перед запуском приложения нужно выполнить какой то произвольный код (подменить / определить значения
переменных окружения, создать файлики и дернуть АПИ) - то можно положить в /bin/pre_start исполняемый файл вида `my-application`.
**Важно:** файлики запускаются утилитой run-parts и по соглашению их имена могут содержать только ASCII буквы, цифры, - и _.

**geobase**
Если приложение использует геобазу - нужно чтобы в Dockerfile приложения была строчка.
`RUN /bin/prepare-geobase.sh`

Для [локальной сборки](https://st.yandex-team.ru/RASPFRONT-8190) с геобазой нужно добавить файл с [OAuth-токеном](https://wiki.yandex-team.ru/sandbox/api/#oauth):
```
COPY docker/.sandbox_oauth_token /.sandbox_oauth_token
RUN /bin/prepare-geobase.sh
```

## Базовый питонячий образ registry.yandex.net/rasp/trusty-python-base

Добавляет некоторые питонячьи зависимости.

## Быстрый старт
Достаточно скопировать содержимое template в корень проекта и поднастроить Dockerfile и конфиги под себя.
```(bash)
cd {my-project-dir}
cp -r ../docker-images/template/* .
```

**Важно:** Обязательно нужно настроить логгирование в соответствии с конфигом logrotate. По умолчанию, считается что
логи пишутся в `/var/log/app`.


### Juggler
Конфиги пишем/правим тут: https://a.yandex-team.ru/arc/trunk/arcadia/travel/rasp/config/juggler/geo_juggler/rasp/
Имя конфига такое же как и у dorblu (qloud-ext.{проект}.{приложение}.{окружение}.{компонент}.yaml).
Документация на конфиги ansible-juggler: https://wiki.yandex-team.ru/geo-infra/components/ansible-juggler/

**Пример конфига:**
Файл: `qloud-ext.rasp.blablacar.production.backend.yaml`
Содержимое:
```yml
- gather_facts: false
  hosts: localhost
  roles:
  - checks:
    - vhost-500
    limits: '{{ crit_0_warn_0 }}'
    role: passive
  vars:
    children:
    - QLOUD%rasp.blablacar.production.backend@type=ext
    host: qloud-ext.rasp.blablacar.production.backend
  vars_files:
  - ../vars/common.yml
  - vars/rasp.yml
```

Где:

    - vars.children - это список групп хостов, с которых мы аггрегируем метрики. (Видно что идентификатор каждой группы
    хостов начинается с магического QLOUD, далее идет путь до компонента и дальше тип (ext/int). В нашем примере тут только одна группа, но их может быть много.
    - vars.host - имя под которым будет светиться проверка, например в телеграмме будет видно `qloud-ext.rasp.blablacar.production.backend:vhost-500` -
    имеет смысл так же указывать полный путь до компонента, чтобы потом было проще искать.

Для того, чтобы проверки включились - необходимо добавить include конфига juggler сюда: `https://a.yandex-team.ru/arc/trunk/arcadia/travel/rasp/config/juggler/rasp.yml`

### Unistat

Unistat-aggregator реализует АПИ yasmagent для приложения, для платформы он реализует АПИ unistat.
Для того, чтобы использовать в проекте - достаточно добавить в nginx конфиг что то вроде вот такой секции:
```
server {
    include listen;
    include auth/allow_yandex_only;

    location /unistat {
        proxy_pass http://127.0.0.1:11005;
    }
}
```
И включить в окружении unistat ручку в GUI qloud, указав соответствующий путь и порт.

## Правила именования qloud окружений

Приложение именуется так, чтоб было понятно, что это такое: touch, old-morda-python, rasp-front.
Основной компонент, обслуживающий трафик называется `main`.
Внутренний балансер окружения должен называться так: {environment}.{application}.{project}.common.yandex.ru, например production.touch.rasp.common.yandex.ru.


## qloudexec.sh

Позволяет выполнить произвольную команду на некотором количестве контейнеров нужного компонента в нужном окружении
и получить вывод комманды.

Использование
```
./qloudexec.sh 12 main-NNN.main.testing.train-api.rasp.stable.qloud-d.yandex.net "free -m"
```
где 12 - кол-во машин, длинная строчка это путь до компонента в окружении, а в конце видна команда free -m.

