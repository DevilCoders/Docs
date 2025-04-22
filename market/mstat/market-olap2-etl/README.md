https://wiki.yandex-team.ru/Market/projects/marketstat/support/olap2etl/

Команда, чтобы задеплоить jar с jdbc вертики в наш артифактори:
```$sh
mvn deploy:deploy-file \
-DgroupId=com.vertica \
-DartifactId=vertica-jdbc \
-Dversion=9.0.1-0 \
-Dpackaging=jar \
-DrepositoryId=yandex_market_releases \
-Durl=http://artifactory.yandex.net/artifactory/yandex_market_releases \
-Dfile=./vertica-jdbc-9.0.1-0.jar
```
