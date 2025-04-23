### Что это?

Бекенд конструктора форм.

### Как начать разрабатывать?

* клонировать репозиторий
```
git clone git@github.yandex-team.ru:tools/forms.git
```
* установить pyenv
```sh
# сделать как описано в https://github.com/pyenv/pyenv#basic-github-checkout
git clone https://github.com/pyenv/pyenv.git ~/.pyenv
# зарегистрировать переменную PYENV_ROOT и обновить пути
echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.bash_profile
echo 'export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.bash_profile
# собрать рабочую версию интерпретатора
pyenv install 3.5.7
pyenv local 3.5.7
```
* собрать virtualenv
```sh
# устанавливаем сам poetry
pip install --user -U poetry
# собираем зависимости
poetry install
```
* скопировать базу postgresql, как описано на странице [Про дамп/восстановление данных с тестинга](https://wiki.yandex-team.ru/forms/dev/testingdump/)
* следовать флоу [Удачная модель ветвления для Git](https://habr.com/post/106912/)

### Как собирать?

Самый простой способ выкатить все приложения в тестинг с созданием новой версии
```
make release
```
Собрать без изменения changelog.md и выкатить в тестинг, необходимо явно указать версию
```
make release v=32.0 nochangelog=1
```
Только собрать версию, без изменения changelog.md
```
make build v=32.0 nochangelog=1
```
Только запушить собранную версию
```
make push v=32.0
```
Выкатить все приложения в продакшен
```
make deploy v=32.0 e=production
```
Выкатить конкретное приложение в продакшен
```
make forms_ext v=32.0 e=production
```

### Как тестировать?

Запустить все тесты
```
./forms_manage tests_boxed
```
Запустить тесты из конкретного приложения
```
./forms_manage tests events/surveyme/
```
Запустить тесты из конкретного тест-файла
```
./forms_manage test events/surveyme/tests/views_api/questions.py
```
Запустить тесты из конкретного тест-кейса
```
./forms_manage tests events/surveyme/tests/views_api/questions.py::MovePageQuestionsTest
```
Запустить одиночный тест
```
./forms_manage test events/surveyme/tests/views_api/questions.py::MovePageQuestionsTest::test_move_page_up
```

### Стенды

Сейчас стенды нужно создавать руками

Создать стенд, из текущей рабочей ветки выполняем команду
```
bin/create_stand.sh
```

Удалить стенд, из текущей рабочей ветки выполняем команду
```
bin/drop_stand.sh
```

При необходимости можно указать имя стенда, например
```
bin/create_stand.sh -s python37
bin/drop_stand.sh -s python37
```

Можно создать стенд для определнного приложения
```
bin/create_stand.sh forms_biz
bin/drop_stand.sh forms_biz
```

А в сочетании с именем стенда будет
```
bin/create_stand.sh -s new_profiles forms_biz
bin/drop_stand.sh -s new_profiles forms_biz
```

### Где старая документация?

* [Документация разработчика](https://wiki.yandex-team.ru/technologies/forms/Yandex.Tech-API-dev/)
* [Документация для потребителя внешнего API](https://wiki.yandex-team.ru/technologies/forms/Yandex.Tech-API/)
* [Документация для потребителя API для админки](https://wiki.yandex-team.ru/technologies/forms/Yandex.Tech-admin-API/)
