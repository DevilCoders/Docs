# Formula Chooser - понятный выбор формул ранжирования средним

## Концепция
1. Вход cgi -> TRequestParams -> InputFlags + mappings-to-use-id

InputFlags - вектор bool переменных, которые управляют flow внутри логики выбора формул (RuleSet-ов)

2. mappings-to-use-id + Mappings -> Ruleset

В файле маппингов каждому id приписан RuleSet который надо использывать. Может быть переопределено в переранжировании.

3. RuleSet + InputFlags -> Deduction = [Stage -> VarName]

RuleSet - описание как из InputFlags получить именна-переменных, для каждой из поддержанных стадий

4. Deduction + mappings-to-use-id + Mappings -> FullDeduction [Stage -> FmlId + VarName]

На последней стадии - резолвим переменные в маппингах (собственно - основное назначение Mappings как раз хранить отображение переменных в конкретные формулы).

Применение логики в рантайме происходит в [переранжировании](https://a.yandex-team.ru/arc/trunk/arcadia/search/web/rearrange/formula_chooser).


## Формат RuleSet-ов
* Каждый rule-set отображает набор флагов в результат (deduction)
* Проверка состоит в выполнении "логическое-И (флаг)" или "логичкое-И (отрицание флага)"
* Если выполнено более одного случая типа Case, то результатом будет ошибка
* Порядок вычиселния такой:
  - все deduce заполняются из Default
  - Проверяются RewritableCase в порядке возрастания EvaluationOrder. Если условия выполнены - Deduce перезаписывают соотв. поля
  - После проверяются все Case (для оних ожидается не более 1 одновременно выполненного условия). Их Deduce пересаписывают соотв. поля

## Как тестировать
* resolve_result_tests::FlagsResolve позволяет проверить дифы на запросах среднего - позволяет проверять
* так же есть тесты для всех возможных значений флагов (ограничение перебора по размерностям задаётся в mmapings_exporter/main.cpp) - позволяет проверять результат резолва, проверять дифы.

## Доставка маппингов
В архив моделей среднего подливается конкатенация от mapping.proto.txt , experimental_rulesets.proto.txt , trunk_ruleset.proto.txt , файлов из папки configs_archive и список имеющихся переменных (т.е. добавлять и менять их можно без необходимости релиза среднего)

Таким образом RuleSet и маппинги, в которых нет новых (для prod-версии среднего) переменных и флагов, выезжают быстро.

При открытии этих файлов выкидываются RuleSet/Mapping в котором нашлись неизвестные значения enum-ов.

Доставка происходит в текстовом формате, enum-ы в числовом виде, чтобы можно было работать с неизвестными переменными (отдельно в архиве катится словарь переменная -> строковое значение). В случае неизвесных флагов, соответствующие рулсеты и маппинги выкидываются.

Если открытие маппингов из архива будет с ошибкой - средним будет сообщена ошибка и случится фолбек на вкомпиленный вариант.

## Управление переранжированием через cgi
Основной режим управления: ```rearr=fon=VAR_NAME-FML_ID```

Например, ```&rearr=fon%3DV_DEFAULT_L3-547520``` означает, что во всех тех случаях, когда система выводит V_DEFAULT_L3, её значением будет 547520.

Для задания сложных переменных надо использывать следующий синтаксис: ```&rearr=fon=V_DEFAULT_PERS-FmlId:547520-Weight:0.45```.

Опция для изменения rule-set выглядит так: ```&rearr=scheme_Local%2FWebFormulaChooser%2FForceRuleSet%3DForceFormula```.

Включить текущую Opt формулу можно так: ```&rearr=scheme_Local/WebFormulaChooser/ForceRuleSet=Opt```.

Выбрать весь маппинг ```&pron=models=web_mmeta:2:339```.
Приоритет 1 используется для выкаток через флаги, для прокачек и прёмок рекомендуется использывать как указано в этом примере - приоритет=2.


## Инструкция по выкатке новой версии маппингов
0. Ответственные за приемки - ilnurkh@, romanenko-ii@.
1. Заведите тикет в очереди WEBQUALITY с тайтлом "Приемка флагов production формул <id>". **Не забудьте добавить в наблюдатели ответственных за приемки!**
2. Создайте ревью с изменениями mappings.proto.txt ( **N.B.** все новые формулы должны находится в prod секциях соответствующих файлов https://a.yandex-team.ru/arc_vcs/search/web/rearr_formulas_bundle/content)
3. Ваше изменение (например, релиз формул или бустов), может изменить порядок использования фичей: либо вы начинаете использовать какие-то новые фичи, либо наоборот ваш релиз призван у меньшить множетсво используемых фичей. В этом случае необходимо призвать в релизный тикет отвественных за эти фичи, чтобы они определили какие теги должны быть у этих фичей, и закомитили необходимые изменения в транк. Здесь же необходимо убедиться, что фичи действительно можно депрекейтить, если такое изменение требуется. В сложных случаях отвественным за формулы необходимо поменять в конвейерах правила зануления фичей.
4. После мерджа нужно выкатить модели среднего. [Ссылка на ci](https://a.yandex-team.ru/projects/relev_tools/ci/releases/timeline?dir=search%2Fruntime_archives%2Fmiddle_search&id=release-mmeta-models). Выкатка осуществляется дежурными по моделями, попросите о необходимости выкатки в [чате релизов формул](https://t.me/joinchat/GqFpP0KTznRPlXDYIh-wkQ))
5. После релиза моделей: запускайте приёмочные графы.
   Как вариант, приемочные графы можно складывать [в эту директорию](https://nirvana.yandex-team.ru/browse?selected=9349197), но строгих правил нет. Если вы выкатываете маппинги в первый раз, то можно склонировать граф приемки с последнего релиза. Для релиза L3 формул через маппинги в приемочных графах мы снимаем два типа серпов: для прод и опт формул.
   Приемочные графы веба и актуальный список приемочных корзин поддерживается в актуальном состоянии с помощью [этого кубика](https://nirvana.yandex-team.ru/alias/operation/get-proximay-gold-items), но если вы сомневаетесь в актуальности кубика, список корзин можно уточнить у ответственных за приемку.
   **N.B.** Дифф приемки следует запускать с дооценкой в квоте Acceptance. Бездифовые приемки можно запускать с дооценкой в квоте High Prioirity.
   Если у вас не хватает прав на дооценки, то после прокачки серпов сгенерятся ACL тикеты, в таких тикетах нужно написать, что дооценка для приемки и прилинковать ваш тикет приемки.
6. После того, как приемка сошлась необходимо оформить краткие результаты в таблицу. Для этого используйте [этот кубик](https://nirvana.yandex-team.ru/alias/operation/mlm-dump-for-priemka). Кубик можно дополнить дополнительными метриками по вашему желанию (при необходимости). [Пример](https://nirvana.yandex-team.ru/flow/2c4f966f-ef8e-43a5-8afe-7fbda74c7842/897f6910-c51d-41e0-8acf-d8d01ec7a11e/graph) как это можно сделать.
7. Далее надо поменять дефолты в  mappings.proto.txt . **Все коммиты должны быть привязаны к тикету**.
    > NOTE: Правила выставлния PreviousDefault (обновить надо **одновременно** с выставление своего флага в дефолт, так как только в этот момент знаете в какую дату планируется выезд)
    >    - Не меняется для изменений, не затрагивающих основные корзины (зеро-дифы web_world_validate), такие как изменения турции, алисы, eu и т.п.
    >    - Не меняется если предыдущий маппинг выезжает в тот же день (два маппинга одним релизом или два маппинга в день двумя релизами)
    >    - В остальных случаях равен версии предыдущего дефолтного маппинга

    > NOTE 2: Если у вас изменение в основной поток, то вы **должны** сообщить об этов в чат приёмки поисковой базы, чтобы они могли переснять приёмку и база не поехала недооценённой (ссылка будет позже. можете просить вас добавить туда в [robotsupport](https://wiki.yandex-team.ru/robot/jupiter/))
8. Потом надо создать релиз в абт. Для этого склонируйте [Sandbox таску](https://sandbox.yandex-team.ru/task/1209916417/view), добавив краткое описание своего релиза. Для запуска нужно быть в этой группе https://sandbox.yandex-team.ru/admin/groups/SEARCH-RELEASERS. Таска сгенерирует test-id с новыми флагами, нужно провалидировать параметры этого тестида, убедиться что выставлены корректные флаги.
9. Прилинковать SEAREL тикет к приёмке (смотреть проще всего тут https://ab.yandex-team.ru/deploying/items#BULK_TESTED)
10. Отправить на выкатку флаги (или попросить того, у кого есть права) через https://ab.yandex-team.ru/deploying/items#BULK_TESTED. Роль в idm "Админка экспериментовФлаги / Общее / Выкатка моделей" . Между созданием test-id и этим шагом должно быть минимальное время. Не создавайте test-id (пункт 9) если не готовы отправить на выкатку, ибо тогда возможен рейс и флаги выедут позже нового релиза и могут его перезатереть.
    > NOTE: На вкладке Deploying должно быть пусто.

    > NOTE: Вечером выезжает [кошерный релиз флагов](https://wiki.yandex-team.ru/serp/experiments/raae2/faq/), собираемый из экспов. Если в релиз отправляете после 16 (или видите что из-за работ поедет после 16) имеет смысл уточнить [в чате выкатки на 100%](https://t.me/joinchat/Tqp1-86s8c9_Bz7f) об их планах и пропустить вперёд их релиз.
11. Лучше явно сообщить о релизе в [чат](https://t.me/joinchat/QBOqnOEY1vqhdmse) ([дежурной смены](https://wiki.yandex-team.ru/jandekspoisk/sepe/dezhurnajasmena/)), чтобы убедиться что релиз не пропустят, примерно таким сообщением
    > Добрый день: тут релиз формульных флагов. https://nanny.yandex-team.ru/ui/#/r/SANDBOX_RELEASE-1226696369-STABLE (ссылку можно найти [тут](https://nanny.yandex-team.ru/ui/#/queues/meta/SEARCHMON/releases/) или в sb таске, ссылка на которую есть в абт-шнице). Сориентируйте пожалуйста когда оно выедет.

    Если релиз пробивает Кэш, то добавьте что

    > Релиз пробивает поисковый кэш на средних веба. Катить нужно после 19, желательно сегодня, либо как можно раньше утром (чтобы после релиза кэш успел набраться)

    Если в релизе дифы sinsig-dcg-5 на валидейте больше 0.25 добавьте

    > Возможны прокрасы дифов, но с релизом пройдёт. Дежурным качества просьба быть готовым подправить пороги абсолютов

    и в дополнении к marty пинганите [дежурных по качеству](https://abc.yandex-team.ru/services/web_quality_duty/duty/)
12. При необходимости заведите обратный эксперимент к выкаченным изменениям. В качестве шаблона обратного эксперимента можно взять последний актуальный обратный эксперимент. Его можно найти в предыдущих тикетах очереди WEBQUALITY.
13. Занесите релиз [в таблицу](https://st.yandex-team.ru/FORMULA-2128#61010faa54483d1dab02951e).
14. Если через маппинги вы релизили L3 формулы, необходимо обновить их [в артефактах Нирваны](https://nirvana.yandex-team.ru/browse?selected=367043). Эти артефакты используются в обучении L3 формул для сравнения с текущим продом. Поэтому после релиза формул обязательно не забыть актуализировать их и в артефактах. Обновить необходимо три артефакта: KubrExussrDesktopTouch, KubrExussrDesktopTouchClick, KubrExussrDesktopTouchOpt.
15. После любого релиза обязательно проставляем комментарии на графики основных KPI метрик. На момент составления этой инструкции основная метрика - `Proxima-v11`, ее KPI график можно найти [здесь](https://nda.ya.ru/t/zPcw3g_A4t6EqT). Релиз может выпасть на время перехода на новую метрику, поэтому может понадобиться проставлять комментарии с релизом и на предыдущие версии метрики. Если вы сомневаетесь в том, на какие метрики проставлять комментарии с вашим релизом, напишите в чат KPI. Если вас в нем нет, попросите добавить ответственных за приемку.
    Комментарий нужно ставить **на следующий день после выкатки**, чтобы скачка, которая случилась в точке уже была с релизом, а предыдущая была без релиза. KPI качается в 6 утра (если всё хорошо), поэтому обычно точку нужно ставить на следующий день после выкатки.
16. Опционально: если ваш релиз как-то связан с проектом Computer Science, то в дополнение к пункту 16 вам необходимо добавить комментарии с релизом на графики CS метрик. Для проекта CS есть две основные метрики - `cs-sinsig-dcg` (ее график можно найти [тут](https://nda.ya.ru/t/M1-TUtgV4wbGeC)) и `apscore-1-win-rate` (ее график можно найти [тут](https://nda.ya.ru/t/rIBhELXO4tpfwW)).
17. Для тех, кто добрался до конца: вы восхитительны!
