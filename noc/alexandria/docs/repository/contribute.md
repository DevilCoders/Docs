## Модификация Matchers и Softs
### Начало
Управление "содержимым", которым оперирует Александрия, происходит через Pull Request в [репозиторий](https://a.yandex-team.ru/arc/trunk/arcadia/noc/alexandria).  
Для этого необходимо [получить код из Arcadia](https://docs.yandex-team.ru/devtools/intro/quick-start-guide).

### Матчеры и ПО
Чтобы изменить ответы Александрии необходимо внести изменения в файл matchers и в файлы softs.

* [matchers.yaml](https://a.yandex-team.ru/arc/trunk/arcadia/noc/alexandria/stash/generator/source/matcher/matchers.yaml)
* [softs в формате yaml](https://a.yandex-team.ru/arc/trunk/arcadia/noc/alexandria/stash/generator/source/soft)

TODO: https://st.yandex-team.ru/NOCDEV-6332

### Базовые проверки ввода
В базовом случае, генератор не пропустит следующие ошибки:
* Нет содержимого matchers и softs
* [Проверки матчеров](https://a.yandex-team.ru/arc/trunk/arcadia/noc/alexandria/stash/generator/matcher.go?rev=r8968468#L77):
  * В матчере одновременно нет фильтров ModelRe и RackCode
  * В матчере нет ссылки на SoftID
  * При добавлении ModelRe необходимо по-особенному обрабатывать обратный слэш из-за особенностей yaml. `\s` -> `\\s` 
* [Проверки файла ПО](https://a.yandex-team.ru/arc/trunk/arcadia/noc/alexandria/stash/generator/soft.go?rev=r9020159#L145):  
  * нет типа файла (Type string yaml:"Type")
  * нет содержимого списка файлов самого ПО (`Files []SoftFile yaml:"Files"`)  
* Матчеры ссылаются на несуществующий SoftID. [Тест на консистентность](https://a.yandex-team.ru/arc/trunk/arcadia/noc/alexandria/stash/genstash/gotest/stash_test.go?rev=r8956265#L27).


### Применение изменений
[Упоминаемые манипуляции с arc](https://docs.yandex-team.ru/devtools/src/arc/workflow#workflow)   
[Упоминаемые манипуляции с ya make](https://docs.yandex-team.ru/devtools/build/ya?searchQuery=ya%20make#ya-make)  
Если пропустить шаги с `ya`, то CI и сборка будут ругаться на ошибках. Это займёт время.

* Отвести Branch 
* Внести изменения
* В директории "arcadia/noc/alexandria" выполнить `ya make -t`
```
~/arcadia/noc/alexandria$ ya make -t
```

* В директории "arcadia/noc/alexandria" выполнить `ya make`
```
~/arcadia/noc/alexandria$ ya make
```

* При проблемах с генерацией(stash/genstash stash/generator) попробовать вызвать бинарь `generate` в собранном `~/.ya/build/build_root...`
* Создать commit и pull request
* Перейти на страницу [noc/alexandria: Alexandria PR testing](https://a.yandex-team.ru/projects/nocdev/ci/actions/launches?dir=noc%2Falexandria&id=my-action)
* Дождаться тестов аркадийного CI "autocheck: Autocheck Precommit Trunk`", см. [Alexandria PR testing](ci.md)
* Получить Ship от ревеьювера.
* Merge
