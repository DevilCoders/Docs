# Нестандартные ситуации в релизах

## Не прилинковались тикеты к релизу { #no-links }

**Решение коротко:** `dt-link-tickets` на ppcdev.

**Подробнее**

Иногда в Трекере ломается автолинковка тикетов, на этот случай у нас есть скрипт `dt-link-tickets`.  
Скрипт смотрит на описание тикета, ищет все похожее на id тикетов в очереди DIRECT и показывает те, которые еще не прилинкованы.
По ключу `--do` прилинковывает тикеты по найденному списку.  
В комментариях тикеты (пока?) не ищет.

Пример использования:

```
# Смотрим список недолинкованного к релизу DIRECT-129437
ppcdevN$ dt-link-tickets DIRECT-129437
to link: 1
DIRECT-129409 Починить тест ClientDataServiceClientInfoForLimitedAgencyRepresentativeTest

# Линкуем недолинкованное
ppcdevN$ dt-link-tickets DIRECT-129437 --do
to link: 1
DIRECT-129409 Починить тест ClientDataServiceClientInfoForLimitedAgencyRepresentativeTest
linked
```

Так выглядит релиз, в котором все тикеты прилинкованы:

```
ppcdevN$ dt-link-tickets DIRECT-129437     
to link: 0
```

Скрипт в репозитории: <https://a.yandex-team.ru/arc/trunk/arcadia/direct/infra/direct-utils/direct-release-tools/bin/dt-link-tickets>


## Нужно отложить выкладку релиза { #postpone-release-deployment }
Если после завершения тестирования релиза понадобилось, чтобы дежурные не выкладывали его в ближайшее релизное окно, нужно проставить релизу заголовок "[НЕ ВЫКЛАДЫВАТЬ] ..." и предупредить дежурных в [админском чате]({{chat-direct-admin}})

```sh
direct-release -a app -s testing rename "[НЕ ВЫКЛАДЫВАТЬ] ..."
```

Не касается dna и NewCI релизов


## Проблемы с тестами или тестовыми данными
Поищи рецепт в разделе: **Руководство (инструкции)** → **Тестирование** → **Решение проблем**.

Если там не нашлось ответа — ищи на вики, спрашивай у коллег.


## Сборка релиза упала { #create-release-failed }
Бывает, что запуск `direct-release --create-release` завершается с ошибкой, например из-за таймаута.
Если падение произошло из-за обновления ТС, можно попробовать разобраться по [инструкции](../jeri/guide/fix-ts-deploy.md)  
Можно попробовать продолжить сборку с того же места, запустив:
```sh
direct-release -a <app> -s testing continue-create-release
```
Для продолжения сборки хотфикса 
```sh
direct-release -a <app> -s testing continue-hotfix
```
Вместо `<app>` нужно вписать своё приложение.  


## Упала автосборка (сборка релиза по крону) { #create-release-auto-failed }
При неудачном завершении автосборки робот напишет об этом в релизный чат [direct-release]({{chat-direct-release}}).  
Пример: `❌ Автосборка релиза direct закончилась неудачно`.

Логи запуска находятся на ppcdev7 в директории `/var/log/yandex/autoreleases/`.

В зависимости от того, как далеко успел зайти процесс сборки релиза, можно предпринять следующие действия:
- попытаться продолжить сборку с места падения

  запустив
  ```sh
  direct-release -a <app> -s testing continue-create-release
  ```

  или же вручную выполнив непрошедшие команды для нужного релиза ([пример для direct](https://a.yandex-team.ru/arc/trunk/arcadia/direct/infra/direct-utils/direct-release-tools/bin/direct-release?rev=r8460014#L806))
  ```sh
  direct-release -a <app> -s testing <cmd>
  ```

  Посмотреть выполненные шаги можно командой
  ```sh
  direct-release -a <app> -s testing show-state
  ```

- завершить текущую неудачную сборку и начать новую

  (если релизный тикет не собрался/не привязались тикеты для тестирования, что происходит на шаге `track`)
  ```sh
  direct-release -a <app> -s testing finish

  dt-autorelease-ctl -a <app> clear-last-try
  ```

  Если окно автоматической сборки релиза уже закрылось, то можно форсировать сборку:
  ```sh
  dt-autorelease-ctl -a <app> force
  ```

Подробности про запуск и форсирование автосборки есть в разделе [сборка релизов по крону](concepts-create-release-auto.md#dt-autorelease-ctl)
