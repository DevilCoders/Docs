Пока тесты не переехали на `ya`, при изменении протолиб необходимо вручную залить новую версию артефакта в artifactory 
и поменять номер версии в `metrika/core/tests/metrika-core-beans/pom.xml`.
Если используется hg или svn и операция проводится в первый раз,
то нужно выполнить в корне аркадии `ya make --checkout -j0 devtools/maven-deploy`

1. В качестве номера версии берется номер текущей ревизии в svn (можно взять из арканума)
2. Сходить в `devtools/maven-deploy/deploy.py` и в `base_cmd` добавить аргумент `--version=<rev_num>` с номером вашей ревизии.
3. Запустить скрипт `deploy_proto.py`
4. Обновить версию либы в `metrika/core/tests/metrika-core-beans/pom.xml`
