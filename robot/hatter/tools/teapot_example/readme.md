Пример бинарника с простым чайником.

В proto лежат протобуфы с данными
В schema/schema.h задаются все нужные имена для чайника
В teapots/piggy/agent.cpp регистрируюся пушеры
В teapots/piggy/*_pusher.cpp лежит бизнес-логика пушеров

**Как запустить:**
Собрать всё
Собрать ads/bsyeti/big_rt/cli/big_rt_cli
Из robot/hatter запустить
`bash tools/teapot_example/bin/create_tables.sh`
Первый запуск может быть долгим.

Стейты:
    * Piggy - стейт с копилками

Очереди пушей:
    * Piggy - очередь с пушами для Piggy


**Piggy Teapot**
Представляет собой именованную копилку. Ей можно задать имя, ей можно инкрементить Value. И то, и другое делается через пуш.

Пушии:
    * SET_NAME: задаёт имя копилке. Можно послать так: `bash ./tools/teapot_example/bin/write_name_push.sh 3 PtolemeyIII`
    * REPUSH: порождает десятисекундный водопад из пушей. Можно послать так: `bash ./tools/teapot_example/bin/write_re_push.sh 3`


