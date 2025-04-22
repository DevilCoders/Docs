# Furita

### Описание
Сервис для работы с пользовательскими фильтрами. API и более подробное описание - можно прочитать [здесь](https://wiki.yandex-team.ru/pochta/backend/furita/)

### Графики

[furita production](https://yasm.yandex-team.ru/template/panel/Furita/application=furita;env=production/)\
[furita-corp production](https://yasm.yandex-team.ru/template/panel/Furita/application=furita-corp;env=production/)

Исходники графиков и алертов расположены [тут](https://a.yandex-team.ru/arc/trunk/arcadia/mail/yasm/lib/furita)

### Окружения в QLOUD

[furita production](https://platform.yandex-team.ru/projects/mail/furita/production)\
[furita-corp production](https://platform.yandex-team.ru/projects/mail/furita-corp/production)

### Сборка
##### Собрать с помощью sanbox-job'ы с прогоном тестов
[CREATE_MAIL_RELEASE](https://sandbox.yandex-team.ru/task/499605603/view)\
Надо запустить с mail_project=furita, джоба прогонит все тесты, соберет docker образ и раскатит его на qa

##### Собрать образ на виртуалке
    ya package  --docker --docker-network=host --docker-repository mail --build=relwithdebinfo --custom-version furita.1.0 --docker-push package/package.json
    
### Логи в Executer
    [Serial] alexandr21> p_exec %mail_furita_production_furita grep something /var/log/furita/furita.log

### ABC сервис
[здесь](https://abc.yandex-team.ru/services/furita/)

### Тесты
[unit](https://a.yandex-team.ru/arc/trunk/arcadia/mail/furita/tests/unit)

[integration](https://a.yandex-team.ru/arc/trunk/arcadia/mail/furita/tests/integration)\
Системные питон-тесты напротив qa-стендов.\
Некоторые тесты могут мигать из-за наличия ожиданий тайминговых событий.

Из корня проекта запускаются так:

```ya make -ttt ./tests/integration/ --test-tag=ya:manual --test-param env=corp```

[isolated](https://a.yandex-team.ru/arc/trunk/arcadia/mail/furita/tests/isolated)\
Все зависимости поднимаются локально. Основаны на devpack.

Из корня проекта запускаются так:

```ya make -tt ./tests/isolated/```

[java prod](https://aqua.yandex-team.ru/#/pack/51dd0b5084ae7d0209a0542c)\
[java corp](https://aqua.yandex-team.ru/#/pack/51defba084ae7d0209ac5cbc)\
Системные java-тесты напротив qa-стендов.\
[26.01.2020] Мигают паки:
* PreviewFieldFromToCcFiltersTest
* ClickerMoveTest
* ClickerDeleteTest
* FilteredFromOtherFoldersTest
* MultipleActionsFilterTest 

После перезапуска остается *PreviewFieldFromToCcFiltersTest*

#### Типичные проблемы:

* Падение с выводом типа

```
Expected: <OK: 4
171418260816790893
171418260816790894
171418260816790896
171418260816790897
>
but: was <OK: 8
168884986026394679
168884986026394680
168884986026394682
168884986026394685
171418260816790893
171418260816790894
171418260816790896
171418260816790897
>
```
Решение: переиндексация тестового пользователя. См. [тикет](https://st.yandex-team.ru/MAILDLV-4217).

### Поддержка tvm 2.0

Смотри [страничку](https://wiki.yandex-team.ru/pochta/backend/furita/#tvm2) фуриты на вики
