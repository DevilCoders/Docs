Запуск теста\
``ya make -t --test-stdout -F test_context.py::test_fill_context``

В тестах используется yatest.common 
https://docs.yandex-team.ru/ya-make/manual/tests/python#yatest \
yatest.common.canonical_file сравнивает файл полученный по итогам теста и каноничный файл
https://wiki.yandex-team.ru/yatool/test/#canonization \
Т.е. результаты теста нужно канонизировать при первом запуске.

Для канонизации одного теста нужно:

! Из директории ``arcadia/market/infra/java-application/mj/v1/generate-project-tool/python-script/tests``
* (необязательно) запустить тест ``ya make -t --test-stdout -F test_package_json.py::test_package_json`` (Тест должен падать с ошибкой, которую вы канонизируете)
* посмотреть результаты в папке ``test-results/py3test/testing_out_stuff/results/<имя_теста>``
* убедиться что результат корректный
* (обязательно) переканонизировать тест, запустив с флагом ``--canonize-tests``:\
``ya make -tF test_package_json.py::test_package_json --canonize-tests``\


Если вы запустили тест не из нужной папки, убедитесь что в ``/java-application/mj/v1/generate-project-tool/python-script/tests/resources/test_service`` нет лишних файлов

При изменении результатов теста их можно переканонизировать ``ya make -AZ``


### pycharm (работает частично)

``ya ide pycharm``

Запуск через pycharm https://clubs.at.yandex-team.ru/python/3392

Некоторые тесты можно дебажить через пайчарм.\
Поможет статья
https://i-dyachkov.at.yandex-team.ru/1 \
Но **не работает** с модулем ``yatest``:
``
AttributeError: 'Config' object has no attribute 'ya'
``\
https://st.yandex-team.ru/DEVTOOLSSUPPORT-11790 \
Ждем https://st.yandex-team.ru/DEVTOOLSSUPPORT-4523
