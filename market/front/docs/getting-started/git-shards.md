# Разворачивание проекта на логрусах с GIT

{% note alert "Внимание!" %}

**ARCADIA Git-Shard's** это (*пока что*) - **эксперементальная технология**
см. подробнее [Arc2Git converter](https://a.yandex-team.ru/arc_vcs/arc/robots/git/readme.md)

При работе с такой версией развертывания проекта вы можете столкнуться с проблемами, багами и артефактами, которые вам придется решать самостоятельно, и/или при помощи **community**, для beta-тестеров этой функциональности есть telegram-чат: https://t.me/+W68GC_iAl1o4YmIy

**Стабильным** и **Поддерживаемым** (командой Инфраструктуры)
является варинат [{#T}](./svn.md)

{% endnote %}


## make_wc

Для того чтобы развернуть проект `arcadia/market/front/apps/marketfront` при помощи технологии **git-shard**
(т.е. как **git**-репозиторий отражающий отдельно взятый каталог **ARCADIA**) вам необходимо воспользоваться
штатной утилитой `make_wc` (доступной в общем пространсве команд на всех логрусах)
- запускаем `make_wc`:

  ![make_wc select project](_assets/git/make_wc_select_project.png)
- выбираем проект `marketfront`;
  далее вам будет предложен диалог (доступный для проектов поддерживающих развертывание в нескольких вариантах VCS)

  ![make_wc select project](_assets/git/make_wc_select_vcs.png)
- выбираем `git`
  ждем выполнения (желательно согласиться на предложенное выполнение **postinstall**-скрипта)
- **PROFIT!!!**

{% note alert "Внимание!" %}

на данный момент, решение для это диалога/этапа - **невозможно установить** через какой либо аргумент вызова `make_wc` - над этим ведётся работа, как говорится "*Coming soon*"

{% endnote %}


{% note info "Как склонировать другой репозиторий на Логрус" %}

Разберём на примере Логруса в Сасове и Кадаврика:

1. `ssh -A market.logrus01hd.yandex.ru`

2. `git clone https://git:$(arc token show)@git.arc-vcs.yandex-team.ru/kadavrique`

{% endnote %}



## Доступные возможности (по сравнению с SVN вариантом)

- переключаться между ветками (**checkout**)

{% note tip "" %}

На уже существующие (залитые в **arc**) ветки, нейминг веток в данном случае **имеет значение**
формат именования веток:
```
users/{юзернейм в аркадии}/{имя ветки}
```
н/п
```
users/ruvata34/test-git-shard-branch
```

{% endnote %}

- создавать ветки (**new branch** и **push**-ить их)

{% note tip "" %}

создавая ветку **обязательно** надо соблюсти формат нейминга:
```
users/{ваш юзернейм в аркадии}/{имя ветки}
```
н/п
```
users/ruvata34/test-git-shard-branch
```

{% endnote %}

- производить обновленеи веток (**pull**-ить, т.е. получать обновления)
- ребейзиться на **trunk**

{% note tip "" %}

в данном случае `trunk` это просто upstream-ветка в текущем репозитории
функциональный аналог привычного `master`

{% endnote %}

----

{% note alert "Dangerous!" %}

на самом деле вы так-же можете
- **коммитить**
**НО!** только с опцией `--no-verify` т.к. [arctick-husky](https://a.yandex-team.ru/arc/trunk/arcadia/frontend/projects/infratest/packages/arctic-husky/README.md) hooks пока не понятно как "поженить" с **git** (будет еще "раскапываться")
- **мержиться** / **ребейзиться** на/с другими веткам (вообщем всё то, что может **git**)
**НО!** надо контролировать процесс и перед пушем ветки историю **обязательно** надо "выпрямлять" (н/п `rebase onto` на актуальный trunk)

{% cut "вредные советы" %}

потенциально в варианте **git**-шарда можно вести разработку и локально
(без маунта **arcadia** в принципе)
чтобы развернуть проект локально, выполняем не хитрую магию:
```git clone https://git:$(arc token show)@git.arc-vcs.yandex-team.ru/marketfront```
подразумевается, что у вас установлен и сконфигурирован **arc**-клиент
**НО!** если вы знаете ваш **arc**-токен, то просто подмените им выражение `$(arc token show)` в вышеописанной команде и тогда **arc**-клиент не нужен тоже (в принципе).
**НО!** без клиента **arc** вы не сможете легко и просто открывать **PR**-ы (веб-интерфейс **Arcanum**-а, увы этого тоже не позволяет)
**НО!** можно воспользоваться **API Arcanum**-а и сделать это при помощи **cURL** запроса
→ [тут](https://docs.yandex-team.ru/arcanum/communication/public-api#sozdanie-pull-requesta)
для этого вам так-же понадобиться **OAuth** токен, получаем его:
→ [тут](https://a.yandex-team.ru/oauth/token)

{% endcut %}

пока что этими возможностями **лучше не пользоваться** (или на свой "страх и риск"),
особенно если вы не уверены в своем понимании ситуации и особенностей работы как с **arc** так и **git**

для использолвания **git**-шардов на логрусах они вам **не нужны**.

{% endnote %}

## Общие принципы работы (ARC локально - Git-shard на логрусе)

{% note tip "" %}

**все команды сборки и запуска проекта (npm script) - работают идентично** вне зависимости от типа **VCS** использованной для развёртывания **ARC** / **SVN** или же **Git**-шард тут не является исключением


{% endnote %}

1. Подразумевается что, вы будете работать с ветками "синхронно".

    {% note info "" %}

    т.е. та-же ветка что у вас установлена **как текущая** (current branch) в **ARC** (локально) 
    \-  установлена таковой и в **Git**-шарде (на логрусе)

    {% endnote %}   

    Таким образом вы можете использовать **SFTP** (ровно в таком-же виде как вы это делали раньше, тот-же `Auto Upload` в IDE должен вести себя предсказуемо)

2. Если ветки выставлены "синхронно" - вы можете коммитить и пушить коммиты в **ARC** (локально)   
\- и **pull**-ить их в вашей ветке в **Git**-шарде (на логрусе) 

    {% note alert "Dangerous!" %}

    как и раньше в схеме с "**Git** локально - **Git** на логрусе", **если ваши ветки не "синхронизированны"**, при обмене файлами по **SFTP**, особенно при `Auto upload` в IDE  
    → Вы можете получить множестов забавных/и не очень артефактов, но тут как говорится: "Куда деваться?"

    {% endnote %}
