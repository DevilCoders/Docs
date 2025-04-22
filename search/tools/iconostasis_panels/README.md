Здесь лежат файлы этих головановских панелек:

* https://yasm.yandex-team.ru/template/panel/web/
* https://yasm.yandex-team.ru/template/panel/images/
* https://yasm.yandex-team.ru/template/panel/crashes/
* https://yasm.yandex-team.ru/template/panel/yandex_tld/
* https://yasm.yandex-team.ru/template/panel/yandex_tld_5xx/

Workflow редактирования панелек
-------------------------------

1. Чекаутим репозиторий с панельками:
    ``svn checkout svn+ssh://arcadia.yandex.ru/arc/trunk/arcadia/search/tools/iconostasis_panels``
2. Редактируем одну из панелек, например "web": ``vim web``.
    Вам может пригодиться [Документация на шаблоны в Ambry](https://wiki.yandex-team.ru/users/yoschi/templates-api/).
3. Загружаем отредактированный файл в Голован по временному имени: ``./panel.sh test web``.
    В конце stdout будет ссылка на временную панельку в Головане.
4. Открываем временную панельку в Головане и проверяем, что панелька ОК.
    Если не ОК, идем обратно к редактированию, на пункт 2.
5. Коммитим измененную панельку в репозиторий: ``svn commit``. Через 1 час панелька будет обновлена
в продакшене автоматически с использованием sandbox-задачи `UPDATE_MARTY_PANELS`. Если вы загрузите изменения
через ``./panel.sh upload``, они будут безжалостно стёрты содержимым, *закоммиченным** в репозиторий.
См. также [DEVOPS-495](https://st.yandex-team.ru/DEVOPS-495).

Параметризация панели "web"
-----------------------------

``https://yasm.yandex-team.ru/template/panel/web/panels=[base];geo=[vla,sas];lights=foo``

Без параметров (с их дефолтными значениями) показываются все графики в трех локациях без светофоров.

Возможные параметры:

* ``geo=[vla,sas,man]`` – какие локации показывать
* ``panels=[l7_fails,report_status,report,templates_profile,sources,apphost,mmeta,mmeta_unanswer,base]``
   – какие панельки/чарты показывать
* ``lights=SomeStringOrNothing`` – при непустом значении, справа от панелек/чартов будут светофоры

Точнее параметры можно посмотреть в файле панельки.

Параметризация панели "images"
-----------------------------

``https://yasm.yandex-team.ru/template/panel/images/panels=[base];geo=[vla,sas]``

Без параметров (с их дефолтными значениями) показываются все графики в трех локациях без светофоров.

Возможные параметры:

* ``geo=[sas,man,vla]`` – какие локации показывать
* ``panels=[l7,report,templates_profile,src_setup,apphost]``
   – какие панельки/чарты показывать
* ``lights=on`` – при непустом значении, справа от панелек/чартов будут светофоры

Точнее параметры можно посмотреть в файле панельки.

Обновление через CI [тут](https://a.yandex-team.ru/projects/dutysearch/ci/releases/timeline?dir=search%2Fmon%2Fupdate_marty_panels&id=update_marty_panels)