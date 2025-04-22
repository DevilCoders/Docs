# Описание генерируемых файлов

#### Схемы для маппинга CaesarHash(banner_id) на диапазоны шардов kvrs, могут использоваться в клиенте kvrs:
prod.kvrs.banner_tier_main.schema.pb.txt - копия закоммичена в https://a.yandex-team.ru/arc/trunk/arcadia/yabs/server/libs/saas/kvrs_banner_schema.txt  
prod.kvrs.banner_resources.schema.pb.txt - копия закоммичена в https://a.yandex-team.ru/arc/trunk/arcadia/yabs/server/libs/saas/testing.kvrs.banner_tier_main.schema.pb.txt  
testing.kvrs.banner_resources.schema.pb.txt  

#### Схемы для маппинга таблетов очереди баннеров в Цезаре на шарды воркеров, могут использоваться для инициализации воркерных стейтов командой init-shards утилиты yt_dynamic_tables:
xdc.saas2-prod-dsp_creative-worker.banner_tier_main.tablet_mapping.schema.pb.txt  
xdc.saas2-prod-dsp_creative-worker.banner_resources.tablet_mapping.schema.pb.txt  
xdc.saas-2-testworker-creative-stage.banner_tier_main.tablet_mapping.schema.pb.txt  
xdc.saas-2-testworker-creative-stage.banner_resources.tablet_mapping.schema.pb.txt  

#### Конфиги воркеров:
xdc.saas-2-testworker-creative-stage.deployUnit.config.pb.txt  
xdc.saas2-prod-dsp_creative-worker.deployUnit.config.pb.txt  
xdc.saas2-prod-dsp_creative-worker.banner_tier_main.config.pb.txt  
xdc.saas2-prod-dsp_creative-worker.banner_tier_resources.config.pb.txt  
