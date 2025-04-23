# Считалка zC для охватного продукта

Считает zc согласно (https://wiki.yandex-team.ru/bannernajakrutilka/targetinggroup/apccheck/).
~~Метод OVERBID (неитеративный) поддерживается напрямую, все остальные - через apc_check, требуют собранного бинарника для работы.~~ Больше не поддерживается, никто им не пользуется, apc_check лучше.

Для охватного видео вся статистика берётся из VideoCompletes лога, поэтому для него поддерживаются следующие действия:
+ показ (`start`)
+ квартили (`q1`, `q2`, `q3`, `complete`)
+ скипы и размьюты (`skip`, `unmute`)
+ LClick (`lclick`)

Для медийки доступен только LClick, статистика берётся из JoinedEFH лога.

Аргументы для вычисления zC:
+ `--range` - даты, для которых считается zC, в формате YYYYMMDD[HH] (например 20210421 или 2021042113). Можно задавать:
  + интервал (`20210416..2021042012`), обе границы - включительные;
  + интервал без правой границы (`20210416..`) - интервал до текущего момента времени (сколько есть логов);
  + одну дату (если без часа - то берётся весь день, иначе только указанный час);
+ `--product-types` - продукты, для которых считается zC (пока поддержаны только `media-creative-reach` и `video-creative-reach`);
+ `--experiment` - номера экспериментов, поддерживается разбиение по ActiveTestIds (префикс `ab`) и PcodeTestIds (префикс `pcode`), эксперименты в свитчере больше не поддерживаются, запускайте эксперименты в АБшнице;
+ `--etalon` - эталонный эксперимент (если не задавать - то будут сравниваться эксперименты против всего остального);
+ `--keys` - поля для формирования группы;
+ `--max-groups` - максимальное число групп (по умолчанию: 2^30);
+ `--conditions` - условия для грепа (пример: `--conditions PageID=1,2,3 ImpID=2`). Условие `FraudBits == 0` добавляется автоматически;
+ `--not-conditions` - условия для грепа по False (т.е. хиты не берутся, если условие верно);
+ `--commerce` и `--not-commerce` - если эти флаги активны, то будут браться только хиты с коммерцией (без);
+ `--action-coefficients` - формулы для вычисления действий, разделены пробелом, внутри формулы коэффициенты перечислены через запятую (пример: `--action-coefficients complete=1.0 lclick=1.0,complete=0.5`);
+ `--method` - метод вычисления zC (по умолчанию: BIDS_RATIO);
+ `--no-paint` - по умолчанию включена прокраска zC (т.е. если интервал в +/- стандартное отклонение не включает 1 - то вывод будет краситься в зелёный/красный), этот флаг отключает прокраску;
+ `--calculate-cost` - [**DANGER**] помимо zC посчитает деньги в эксперименте также, как это делает `exp_stats`, и zC * cost. Использовать с осторожностью, перепроверяя результат с `exp_stats` (должно с высокой точностью совпадать);

Для запуска в Sandbox:
+ `--run-in-sandbox` - флаг запуска задачи в Sandbox;
+ `--vault-secret` - секрет в Yav для запуска (не `uuid`, например `alex-serov_ml_engine_app_token`);
+ `--secret-key` - какой токен достать из секрета (по умолчанию пытается достать `nirvana-secret`);
+ `--owner` - хозяин таски в Sandbox (по умолчанию запускается в личной квоте);

Преимущества запуска в Sandbox:
+ не нужен `tmux`, `screen` или что-то подобное, можно запустить несколько процессов и заняться чем-то ещё;
+ не захламляется диск временными гигабайтными файлами;
+ распараллеливается запуск `apc_check`;

Впрочем, запуск задач в Sandbox имеет заметный оверхед и может придётся стоять в очереди, так что для быстрых расчётов следует предпочесть локальный запуск.

Прочие аргументы:
+ `--apc-check-args` - аргументы для `apc_check` (будут поданы as-is);
+ `--apc-check-path` - путь к собранному `apc_check`;
+ `--dry-run` - напечатать аргументы и выйти, ничего не считая;
+ `--keep-zc-temp-files` - если опция активна, то временные файлы на локальной машине не будут удаляться после завершения работы;
+ `--log-level` - одно из {`debug`, `info` (по умолчанию), `warning`, `error`} - минимальный уровень логирования;
+ `--yt-pool` - пул для вычислений;
+ `--yt-proxy` - кластер, на котором лежат логи (по умолчанию `hahn` и почти всегда это `hahn`, но вдруг);
+ `--no-test-apc-check-call` - флаг пропуска проверки наличия собранного бинарника `apc_check`;
+ `--only-prepare-tables` - флаг пропуска вычисления zC (будут подготовлены таблицы на YT, на этом выполнение закончится);
+ `--copy-final-tables-to` - путь на YT для хранения итоговых таблиц;
+ `--copy-exp-stats-to` - путь к файлу, в который запишется необходимая статистика экспериментов;
+ `--yt-data-weight-per-premap` - YT-спека, предпочтительный размер джобы на этапе вычисления APC и ставок;
+ `--yt-data-weight-per-split` - YT-спека, предпочтительный размер джобы на этапе разбиения таблиц на эксперименты;
+ `--yt-data-weight-per-presort` - YT-спека, предпочтительный размер джобы на этапе сортировки таблиц;
+ `--yt-data-weight-per-stat-calc` - YT-спека, предпочтительный размер джобы на этапе вычисления статистики экспериментов;


Примеры запуска:
`YT_PROXY=hahn ./reach_zc_calculator --range 20210224.. --experiments ab329166 ab329167 --etalon ab329089 --keys OrderID --product-types video-creative-reach --action-coefficients complete=1.0 complete=1.0,lclick=1.0 --conditions VideoFormat=midroll,preroll,postroll VideoKind=instream --not-conditions OrderID=158938779 --yt-pool ads-research`

`YT_PROXY=hahn YT_LOG_LEVEL=WARNING ./reach_zc_calculator --range 20210406..20210409 --experiments ab350891 ab350892 --etalon ab350891 --commerce --keys OrderID --product-types media-creative-reach --action-coefficients lclick=1.0 --yt-pool ads-research`

`YT_PROXY=hahn YT_LOG_LEVEL=WARNING ./reach_zc_calculator --range 20210403..20210407 --experiments ab350386 ab350388 --etalon ab350386 --keys OrderID --product-types video-creative-reach media-creative-reach --action-coefficients complete=1.0 lclick=1.0 lclick=10.0,complete=1.0 --yt-pool ads-research`

`YT_PROXY=hahn ./reach_zc_calculator --range 20210417..2021041812 20210422.. --experiments ab355384 ab355385 --etalon ab355384 --keys OrderID --product-types video-creative-reach --action-coefficients complete=1.0 lclick=1.0 --yt-pool ads-research --method bids_ratio`

`./reach_zc_calculator --range 20210521..20210525 --experiments ab363940,ab363941,ab363942 ab363943 ab363944 --etalon ab363940 --keys OrderID --product-types media-creative-reach --action-coefficients lclick=1.0 --yt-pool ads-research --method bids_ratio --calculate-cost --log-level warning`

`./reach_zc_calculator --range 20210616..20210628 --experiments ab374500,ab374501,ab374506 --etalon ab374500 --product-types video-creative-reach --keys OrderID --max-groups 1073741824 --action-coefficients lclick=1.0[EShowType==LongClicks],complete=1.0[EShowType==Completes] --calculate-cost --commerce --yt-pool ads-research --yt-proxy hahn --run-in-sandbox --vault-secret alex-serov_ml_engine_app_token --owner ML-ENGINE`
