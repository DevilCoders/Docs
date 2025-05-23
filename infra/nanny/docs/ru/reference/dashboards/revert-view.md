# Group Revert View

## Что это? {#what}

View для массового изменения текущих снэпшотов сервиса. Дополняет интерфейс [дашбордов](tutorial.md).

Упрощает процедуру отката релизов. Компактно представляет группу сервисов и связанных с ними релизов. Позволяет выбрать снэпшоты этих сервисов в качестве текущих, чтобы затем запустить откат группы сервисов из дашборда метарецептом.

Исходный тикет: [SWAT-3469](https://st.yandex-team.ru/SWAT-3469).

## Как открыть? {#how-to-find}

1. С дашборда по кнопке **Revert** можно перейти на **Revert View** по всем сервисам.
1. С дашборда по кнопке **Revert View** напротив отдельной подгруппы сервисов — можно перейти на view для этой конкретной группы сервисов.

Дашборд для примера:
![view.png](https://jing.yandex-team.ru/files/sshipkov/view.2bae995.png)

## Как это работает? {#how-does-it-work}

1. Подгружаются последние 5 (число настраиваемо) снэпшотов всех сервисов;
1. Из них достаются релизы;
1. Эти релизы отображаются в верхней части **Revert View**.
![releases.png](https://jing.yandex-team.ru/files/sshipkov/releases.3cdee62.png)

## Как использовать {#how-to}

### Простой случай {#simple-case}

Нужно откатить один единственный релиз, который был вкоммичен последним.

1. Открываем дашборд, переходим с него на **Revert View** (например, по кнопке **Revert**). Мы видим 5 последних снэпшотов каждого сервиса и релизы из которых все эти снэпшоты были созданы.
1. Выбираем последний релиз, нажав кнопку **FROM**.
1. При этом мы увидим на какой именно снэпшот мы будем откатываться в каждом из сервисов.
    ![revert.png](https://jing.yandex-team.ru/files/sshipkov/revert.35b79fa.png)
1. После этого жмём **Revert** на этом релизе;
1. Жмём Apply во всплывшем модальнике;
1. После этого HEADы сервисов будет передвинуты на снэпшоты, на которые мы хотим откатиться, осталось выкатиться;
1. Переходим в дашборд, запускаем деплой своим любимым рецептом.

### Сложный случай {#hard}

Последовательно вкоммичено три релиза, хочется откатить второй из них.
В этом случае нам нужно сначала сделать **Revert** на снэпшоты первого вкомиченного релиза, а затем **Reset**нуть тикеты третьего и вкоммитить их заново. Как это делаем:

1. Так же, как в предыдущем пункте переставляем HEADы на снэпшоты, созданные из первого релиза, но не запускаем деплой;
1. Переходим обратно на дашборд, находим релиз, вкоммиченный третьим;
1. Делаем **Reset** тикетов этого релиза;
1. Жмём на этом релизе кнопку **Commit**;
1. Запускаем deploy нужным рецептом.

