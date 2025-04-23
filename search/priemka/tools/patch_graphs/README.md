# Скрипт для патчинга графов (web, web_noapache_setup, web-setup-batch-sequential)
* Заменяет набор источников (--sources-list) на FROZEN_SERVANT
* Добавляет _dump_source_request и _dump_source_response для NOAPACHE_SETUP,SETUPS
* Патчит timeouts для графов ('webX', 'init', 'web5b', 'adv-machine-search-sources', 'adv-machine-banner', 'web-setup-batch-sequential', 'begemot-workers')
