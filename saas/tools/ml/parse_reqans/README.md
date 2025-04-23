# parse_reqans

Утилита для парсинга факторов из reqans лога.
Код скопипащен отсюда, чтобы научиться применять его для сервисов, отличных от ydo_portal: https://a.yandex-team.ru/arc/trunk/arcadia/ydo/tools/util/parse_logs/main.cpp

## Как пользоваться: 

1. Скачать базу ipreg https://sandbox.yandex-team.ru/resources?hidden=true&type=IPREG_EXPORT&limit=20
2. Запустить эту тулзу:
```console
./parse_reqans --service ydo_portal --reqans_table //home/logfeller/logs/saas-reqans-log/30min/2021-03-14T12:30:00 --output_table ydo_portal2 --output_dir //home/saas/test_odinmillion --ipreg /home/odinmillion/parse_reqans/ipreg
```

## Пример вывода
```console
{
    "factors" = {
        "f_clicks_count" = 426.;
        "FieldSet2Bm15FLogK0001" = 0.7965899705886841;
        "f_frc_spec_chat_clicks_long" = 0.5055850148200989;
        "_CM_Sy_z_specs_descr" = 0.;
    };
    "position" = 0u;
    "reqid" = "1615715998425674-91002810666925395600149-man2-0302-man-shared-app-host-20030";
    "parent_reqid" = "1615715998425674-91002810666925395600149-man2-0302-man-shared-app-host-20030";
    "card_id" = "https://yandex.ru/uslugi/search?worker_id=f1c97b03-485d-4caf-aba3-f8140b663ea8&worker_hash=10647503722295573106";
    "query" = "\xD0\x98\xD0\xB7\xD0\xB3\xD0\xBE\xD1\x82\xD0\xBE\xD0\xB2\xD0\xBB\xD0\xB5\xD0\xBD\xD0\xB8\xD0\xB5 \xD0\xB4\xD0\xB8\xD0\xB2\xD0\xB0\xD0\xBD\xD0\xBE\xD0\xB2 \xD0\xBD\xD0\xB0 \xD0\xB7\xD0\xB0\xD0\xBA\xD0\xB0\xD0\xB7";
    "region" = 194;
};
```
