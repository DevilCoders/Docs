# panoramas

## Описание проекта
https://st.yandex-team.ru/AUTORUAPI-6273

Panoramas – внутренний сервис; служит для обработки и представления в удобных форматах панорам, загруженные пользователями.

### Configuration

Конфигурация состоит из внешнего `datasources` и файла конфигурации проекта `.conf`.

при инициализации - `datasources` и `.conf` проекта мержатся между сабой.
`.conf` проекта имеет приоритет, таким образом появляется возможность переопределить в нем значения из `datasources`  

`datasources` - содержит имена хостов, их портов, все "пароли и явки", т.е. ту конфигурацию которая должна храниться
за приделами самого проекта. по умолчанию путь к `datasources` 
_/etc/yandex/vertis-datasources/datasources.properties_.
на виртуальные машины распространяется автоматически. Для внесения изменений требуется PR в <https://github.com/YandexClassifieds/vertis-ansible>

файл конфигурации `.conf` проекта хранит конфигурацию самого проекта. как пример - имя проекта, конфигурация akka и т.п.
путь к файлу конфигурации строится по шаблону _<имя модуля>/src/main/resources_

файл конфигкрации может иметь версию для окружений: _прод_, _тест_, _дев_ и локального запуска
 
именования конфига:
+ **application.conf** - содержит конфигурацию для продакшен окружения  
+ **application.testing.conf** - содержит конфигурацию тестого окружения  
+ **application.development.conf** - содержит конфигурацию дев окружения
+ **application.local.conf** - содержит конфигурацию локального окружения. **!!! находится в gitignore и в репозиторий попадать не должен**

в проекте может быть как один конфиг, так и несколько для каждего из окружения.

файлы конфигурации мержаться в порядке указанном выше. т.е. если хочется переопределить параметр из продовского конфига application.conf в деве,
его нужно указать в application.development.conf

в свою очередь файлы конфига мержатся между зависимыми модулями.

так вся общая конфигурация определена в модуле `сore` в файлах _core/src/main/resources/*.conf_ и автоматом буде "подтянута"
во все зависимые от него другие модули

чтобы запускать проект локально, надо добавить софт линк на файл scheduler/assembly/docker/select_view.py в каталог проекта

ln -s scheduler/assembly/docker/select_view.py ./select_view.py

### Host's
prod: http://panoramas-api.vrts-slb.prod.vertis.yandex.net  
testing: http://panoramas-api.vrts-slb.test.vertis.yandex.net

### Swagger
http://panoramas-api.vrts-slb.test.vertis.yandex.net/swagger/?url=/api-docs

### Team City
https://t.vertis.yandex-team.ru/project.html?projectId=VerticalsBackend_Panoramas&tab=projectOverview

### Jenkins
https://j.vertis.yandex-team.ru/job/Deploys/job/Panoramas-Api/

### MDB
prod: https://yc.yandex-team.ru/folders/fooqm2o1sunm8jknjhkc/managed-mysql/cluster/mdbandqnv7flt9k4v537  
testing: https://yc.yandex-team.ru/folders/fooqm2o1sunm8jknjhkc/managed-mysql/cluster/mdb0q9tnhf47htih2nvi

testing: https://yav.yandex-team.ru/secret/sec-01drh40th8w227zdbx770ad5jh/explore/versions  
prod: https://yav.yandex-team.ru/secret/sec-01drh5zrnvysg94j5a8rzr5syz

#### git-hooks
To enable git hooks you need to cd to `<project directory>/tools/hooks` and run
`chmod +x setup-git-hooks.sh && ./setup-git-hooks.sh`

If you need to update hooks, just run `./setup-git-hooks.sh` after pulling changes from github.
