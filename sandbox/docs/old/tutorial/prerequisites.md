Чтобы начать разрабатывать задачи для Sandbox, вам понадобятся:

**Виртуальная машина или ноутбук с Linux**. Если у вас нет ни того, ни другого — заведите виртуалку в QYP по [нашей инструкции](https://wiki.yandex-team.ru/sandbox/allocate-host/). В любом случае, на хосте должен быть `ssh-agent` с загруженным в него ssh-ключом со Стаффа ([подробнее](https://wiki.yandex-team.ru/diy/linux/ssh/)).

**Аркадия:** код задач в Sandbox лежит в общем репозитории Яндекса. Вам необходимо научиться с ним работать через одну из систем контроля версий:

* Arc: для первоначальной настройки следуйте [документации](https://wiki.yandex-team.ru/arcadia/arc/). Директория `sandbox` в репозитории появится автоматически.
* SVN: склонируйте минимальную копию Аркадии, после чего загрузите директорию `sandbox`. См. также [документацию](https://wiki.yandex-team.ru/arcadia/starterguide) про использование SVN.
  ```bash
  svn cat svn+ssh://arcadia.yandex.ru/arc/trunk/arcadia/ya | python - clone 
  svn up -q arcadia/sandbox
  ```

В любом случае, проверьте, что вам доступно всё содержимое директории `arcadia/sandbox`.

**Утилита `ya`**, которая лежит прямо в корне Аркадии: `arcadia/ya`. Если вы выполнили предыдущий шаг, она у вас уже есть. Для удобства запуска, сделайте на неё символическую ссылку из PATH-директории, либо алиас в шелле. См. также [документацию](https://wiki.yandex-team.ru/yatool/) утилиты.
