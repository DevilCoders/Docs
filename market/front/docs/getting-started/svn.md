{% note info "" %}

Более подробная документация - находится в разработке...
**Coming soon**

{% endnote %}

# Разворачивание проекта на логрусах с SVN

* [Дока про жизнь с svn на логрусах](https://wiki.yandex-team.ru/users/dgudenkov/svnlogrus/)

## SVN

* Переключение ветки: **возможность отсутствует**.
* Ресет изменений на сервере: `svn revert --recursive .` в корне проекта
* Список изменённых файлов: `svn st | grep ^M` (При этом новые файлы в эту выборку не попадут, поскольку имеют статус `?`)
* Подтянуть свежий trunk: `svn up`
