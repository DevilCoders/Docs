# Репликация датасетов

В связи с тем, что появился запрос на возможность репликации данных между окружениями ecstatic мы поддержали целых 2 механизма репликации.

![replication](../img/replication.jpeg "Вот вам репликация")

## 1. Репликация не реалтайм датасетов

Для репликации датасетов, генерируемых реже, чем раз в час, используется sandbox. Есть 2 шедуллера, запускающих таски раз в час:
    
1. [В тестинг](https://sandbox.yandex-team.ru/scheduler/696309/view)
2. [В дататестинг](https://sandbox.yandex-team.ru/scheduler/696310/view)
3. [В анстейбл](https://sandbox.yandex-team.ru/scheduler/699087/view)

Для подключения такого метода зеркалирования датасетов необходимо в конфиге ecstatic целевого окружения написать следующее:

```
replicate {dataset_name} from {ecstatic_environment}
```

После этого следующий запуск таски репликации подхватит изменения и начнет синхронизировать датасет

## 2. Репликация реалтайм датасетов

Для репликации быстрых датасетов(например, пробок) используется специальный сервис [Bifröst](https://a.yandex-team.ru/arc_vcs/maps/infra/ecstatic/bivrost).

В данный момент доступна репликация только из stable в datatesting. Если вам нужна репликация из stable в testing, приходите к команде инфраструктуры - мы все сделаем

Для подключения репликации неодходимо:

1. В [stable конфиг ecstatic](https://a.yandex-team.ru/arc_vcs/maps/config/ecstatic/stable/maps-core-ecstatic-bivrost.conf) добавить деплой датасета на сервис
2. В [datatesting конфиг ecstatic](https://a.yandex-team.ru/arc_vcs/maps/config/ecstatic/datatesting/maps-core-ecstatic-bivrost.conf) добавить `tvm:2023898` в качестве генератора
3. В [конфиг template-генератора](https://a.yandex-team.ru/arc_vcs/maps/infra/ecstatic/bivrost/docker/install/etc/template_generator/config.d/bivrost.yaml?rev=fe4ee2b2f10f5eebfdbdf5143edcaced47bec317#L9) дописать название датасета
4. Вкоммитить все это добро
5. Попросить команду инфраструктуры выкатить свежесобранный докер
