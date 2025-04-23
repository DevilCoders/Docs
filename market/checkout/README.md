# Checkout Backends

Бэкэнды покупки.

[Wiki](https://wiki.yandex-team.ru/market/marketplace/Dev/)

[Графики](https://grafana.yandex-team.ru/playlists/play/70)

### Информация для контрибьютеров
Feature-ветки необходимо отводить от master и в создаваемых PR-ах указывать базу мержа - master. 
PR будет смержен после аппрува и прохождения всех проверок. Когда ваша ветка смержена в master, можно считать, что тикет выедет в ближайшем релизе.

* В заголовке PR-а и всех коммитах в ветке обязательно должен быть указан тикет из очереди MARKETCHECKOUT. Например, `MARKETCHECKOUT-12345 Очень важные изменения`.
* Любые изменения в коде должны быть покрыты позитивными и негативными тестами. Единственное оправдание отсутствия тестов - hotfix.
* Код миграций должен соответствовать [рекомендациям](https://wiki.yandex-team.ru/users/ivvakhrushev/dbmigrationswithoutdowntime/).
* CheckouterProperties должен использоваться только для временных переключателей потенциально опасной функциональности. После переключения поле из CheckouterProperties должно быть удалено.
* Новые бины (за исключением ZK тасок) должны создаваться только через java config.
* Не использовать Reflection билдеры для toString, hashCode, equal. Можно использовать шаблоны в idea - `MoreObjects.toStringHelper` и `java.util.Objects` equals и hashCode
* Использовать актуальные возможности java (List.of, var, LocalDateTime вместо Date, List/Set вместо массивов)
* Проверьте названия классов, enum'ов, полей на опечатки.
* Код должен содержать информативные логи, по которым должно быть 100% понятно, что произошло. На уровне info не рекомендуется логгировать весь объект, достаточно id или diff.

### Пайплайны

[Катается через CD](https://tsum.yandex-team.ru/pipe/projects/checkout/delivery-dashboard/checkouter-cd-pipeline).

# market-notifier

Уведомления пользователям и магазинам о статусах заказов на Маркете и арбитраже. Использует Checkout-storage.

[Wiki](https://wiki.yandex-team.ru/market/marketplace/dev/market-notifier)

[Графики](https://grafana.yandex-team.ru/dashboard/db/market-notifier)

# Клиенты:

Релизятся автоматически после каждой выкладки.

### Локальные тесты

Локальные тесты могут падать, если на компьютере часовая зона отличается от Москвы.

