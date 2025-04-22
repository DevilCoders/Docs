## TsarBench ##

Бенчмарк юзерной части царей.

### Запуск ###
```shell script
./bench \
    --model_path ~/arcadia/yabs/models_services/libs/models/hit/ut/model_x \
    --yt_table //home/bs/users/blv1mk/crosscheck_sep28/joined_log \
    --model_case 22 \
    --num_workers 4 \
    --model_gen 1
```

Обязательные опции:
* `--model_path <local_path>` - путь к дампу модели
* `--yt_table <yt_path>` - путь к таблице с тестовыми записями; нужны поля `ProfileDump, ShowTime`, протобуф пейджконтекста заполняется отдельно в соответствующей функции. Часто основная часть нагрузки сидит именно в профиле пользователя, поэтому контест можно игнорировать (в модель будет подставляться пустой)
* `--model_case <model_id>` - номер модели в [протобуфе](https://a.yandex-team.ru/arc/trunk/arcadia/ads/bsyeti/libs/tsar/proto/config.proto?blame=true&rev=r8694664#L144)

Другие опции
* `--num_workers <threads|default=std::thread::hardware_concurrency() - 2>` - число потоков
* `--model_gen <model_type|default=0>` - тип дампа модели: 0 - модель из eagle, 1 - hit-модель из сервиса моделей без сплита
* `--use_page_context <0/1|default=0>` - варить ли PageContext
* `--num_rows <num|default=4096>` - на скольких записях лога прогонять бенчмарк
