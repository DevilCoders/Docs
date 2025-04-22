#  Запуск tms локально

## Инструкция
1. В проекте [mbi](https://a.yandex-team.ru/arc/trunk/arcadia/market/mbi/mbi) открыть модуль [mbi-billing](https://a.yandex-team.ru/arc/trunk/arcadia/market/mbi/mbi/mbi-billing), прочитать README.md.
2. Создать Run Configuration в IDEA согласно ридми файлу выше.
3. Запустить и увидеть, что падает, потому что не хватает кредов для etcd. [Их можно взять из Аиды](https://wiki.yandex-team.ru/users/s-ermakov/lokalnyjj-zapusk-s-etcd-datasorsami/#kakzapustit) (_в случае возникновения ошибки_ `ssh: Could not resolve hostname aida: Temporary failure in name resolution` _можно попробовать указать имя хоста полностью, например aida.market.yandex.net_)
4. Добавить креды etcd в Run Configuration -Detcd_username=***** -Detcd_password=******
5. Запустить и подождать несколько минут (на варнингы и ru.yandex.monlib.metrics.labels.validate.InvalidLabelException: value is empty можем не обращать внимание)
6. Чтобы проверить успех, введите команду `echo 'env type' |nc 127.0.0.1 13713`. В результате должно вывести development

Заполненный RunConfiguration выглядит [так](https://jing.yandex-team.ru/files/va-goncharov/Screenshot%202021-06-18%20at%2010.35.12.png)

## Установка Docker
Для работы с market-billing-tms может понадобиться Docker. На Mac OS X его установить можно с официального сайта
приложения [https://docs.docker.com/docker-for-mac/install/](https://docs.docker.com/docker-for-mac/install/). Выберайте
версию подходящую под свой процессор.
