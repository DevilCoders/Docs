Для генерации основных сущностей в dev окружении для PromoHack используйте следующие скрипты:
1. `promo_hack_generate_data_catdir.sql` - создание основных сущностей (localDeveloper с правами Катдира)
2. `promo_hack_generate_data_catdir.sql` - создание основных сущностей (localDeveloper с правами Катмена FMCG)

Для подключения к локальной базе используйте параметры из `src/main/properties.d/local/00_application.properties`

**ВАЖНО: не используйте скрипт для тестинга и прода, это чревато потерей всех данных!!!**
