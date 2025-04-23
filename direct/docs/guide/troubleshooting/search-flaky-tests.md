# Как определить FLAKY-тесты

Иногда CI определяет состояние юнит-тестов в модуле как FLAKY (отмечено оранжевым восклицательным знаком).
Выглядит это вот так:  
![alt](_assets/flaky-tests.png "Вид теста в CI")
За кликом по ссылке **Details** можно увидеть количество тестов:  
`2691 tests: 2657 - GOOD, 4 - SKIPPED, 30 - FLAKY`

Обычно такое происходит с тестами, название которых меняется от запуска к запуску.  
В некоторых случаях проблемные тесты легко обнаружить по их названию: в нём содержатся ID объектов или текущее время.

Для остальных случаев — эта инструкция.  
Рассмотрим на примере юнит-тестов модуля
[direct/libs-internal/grid-processing/ut (java)](https://ci.yandex-team.ru/test/bb30bfd973743963be04e75d2646bf5c?compress_history_by_status=0&limit=50&offset=0)
на ревизии 7168263.

{% note info %}

Инструкция проверена под MacOS.

Нужные утилиты можно установить через Homebrew:  
`brew install zstd wget`

{% endnote %}

## Получение списка тестов
Общая команда для получения всех списков тестов такая:  
`wget -O- --no-check-certificate <ссылка_на_архив_с_логами> | zstd -d  --stdout | grep -aoE '^verify: Test .*' | sort > <файл>`

Кликаем ссылку **Details** у проблемной ревизии.
Появится ряд ссылок на логи, нас интресуеют `logsdir_run1` и `logsdir_run2`.

{% note warning %}

Обе ссылки будут заканчиваться на `/` — нам нужно использовать ссылки без этого символа.  
Если подставить ссылку как есть, то случится ошибка `std: /*stdin*\: unsupported format`.

{% endnote %}

Копируем ссылку `logsdir_run1`, удаляем слеш на конце, подставляем в команду и получаем первый список тестов:  
`wget -O- --no-check-certificate http://download-distbuild.n.yandex-team.ru/mds/2177526/results_merger-7574340166312544441-0-2AC-466642/direct/libs-internal/grid-processing/ut/test-results/grid-processing-ut/testing_out_stuff/1/testing_out_stuff.tar.zstd | zstd -d  --stdout | grep -aoE 'verify: Test .*' | sort > flaky1`

Копируем ссылку `logsdir_run2`, удаляем слеш на конце, подставляем в команду и получаем второй список тестов:  
`wget -O- --no-check-certificate http://download-distbuild.n.yandex-team.ru/mds/1504847/results_merger-7574340166312544441-0-2AC-466642/direct/libs-internal/grid-processing/ut/test-results/grid-processing-ut/testing_out_stuff/2/testing_out_stuff.tar.zstd | zstd -d  --stdout | grep -aoE 'verify: Test .*' | sort > flaky2`

## Определяем различия
Выполняем команду:  
`diff -u flaky1 flaky2 | sort -k 1.2 | less -S`  

{% cut "Пример её вывода" %}

{% include notitle[diff](_includes/flaky-tests-diff.md) %}

{% endcut %}

<br/>
Используя горизонтальную прокрутку — можем увидеть следующие проблемы:

- в тесте **CampaignAccessServiceWalletTest.testGetActions** мигают значения полей:
  - `disabledSsp=["MobFox","Smaato"]`
  - `disabledSsp=["Smaato","MobFox"]`
  - `disabledDomains=rambler.ru,vk.com`
  - `disabledDomains=vk.com,rambler.ru`
- в тесте **AdGroupGraphQLServiceAddTargetingsTest.addInternalAdGroupTargeting** заметить проблему сложнее, но она есть — мигает порядок значений:
  - `value=[1021110101545123184, 2021110101545123184]`
  - `value=[2021110101545123184, 1021110101545123184]`


## Что делать

### Простой случай
Тесту на вход подается коллекция без гарантированного порядка (например Set).  
Дальше она может попадать в модель данных, её `toString`, а с ним — в название теста.

В таком случае нужно использовать коллекции со стабильным порядком.

### Сложный случай
Все входные данные теста имеют стабильный порядок.  
Нужно искать преобразование данных в коде, которой дает нестабильный порядок и исправлять его.

{% note warning %}

Подобные проблемы влияют не только на юнит-тесты, но и на продакшн!

Из-за несовпадения сериализованных моделей у нас может возникать лишняя нагрузка: обработка в ESS, отправка в БК.

{% endnote %}
