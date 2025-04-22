#Java adopt
Здесь расположены референсные состояния файлов nginx-конфигураций для динамического включения/исключения в контейнерах деплоя.

По-умолчанию в `dev`-конфигурациях все конфиги из этой папки включены, однако в деплойной конфигурации они не включены из этой папки,
а подключаются как динамические ресурсы с маской `java-adopt-*.conf`

[continue on wiki](https://wiki.yandex-team.ru/partner/w/dev/infrastructure/systems/applications/partner/java/partner2-nginx-2java-redirect/)
