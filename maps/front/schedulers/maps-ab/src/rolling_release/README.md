## Скрипт для раскатки экспериментов на 100% через Трекер

### Создание выборок и экспериментов

В трекере в очереди `MAPSPRODUCT` для типа задачи "Эксперимент" появились:
-  кнопки `IOS` и `ANDROID`. Появляются в статусах  `В работе` и `Ready for Development`
- локальные поля в группе Эксперимент. Они используются скриптом, запрещено их править напрямую.
- Тэги `ios_processing` и `android_processing`, которые ставятся и удаляются автоматически.  Обозначают что скрипт будет обрабатывать этот тикет

1. Нажимаем на одну из кнопок `IOS` или `ANDROID`
2. выпадет модальное окно, где уже предзаполенны поля:
    - Регионы
    - Версия `ios/android` (детальнее [здесь](https://wiki.yandex-team.ru/maps/analytics/mobile/experiments/newexp/requestform/#pravilazadanijaprostye))
    - Флаги выборок
    - Процент раскатки
    - Отправить на рассмотрение (Его нужно установить в "Да" тогда и только тогда, когда хотим выкатывать заявку в прод на указанный процент)

3. Меняем нужные поля
4. Нажимаем кнопку "Применить"
5. Зупускается скрипт в `Nirvana`, который
    - Создаст выборку
    - Создаст эксперимент в статусе `Черновик`, привяжет созданную выборку
    - Отпишет комментарий с приложенными ссылками эксперимента и выборки
6. Если хочется поменять что-то, также открываем модальное окно и правим. Происходит тоже самое. (Можно править выборку и эксперимент только в статусах `Черновик/На утверждении`)
7. Как только вы готовы отдать заявку на рассмотрение, выбираем в селекте "Отправить на рассмотрение" вариант "Да" и жмем применить. Пока заявка не попала в очередь ее еще можно править (она будет откачена в черновик, отредактирована и обратно возвращаена "На рассмотрение")

PS: <b>ВАЖНО: Если двое редактируют одновременно, выбирается человек, который правил последний. Если у него нет прав, то все изменения в трекере откатятся до значений в Админке. Если есть права все обновится. Лучше избегать этого кейса</b>

PPS: <b>ВАЖНО: предлагаю сейчас дожидаться всегда ответа от робота прежде чем править еще что-то. Хочется проверить всю логику. Потом будем ассинхронно править</b>


PPPS: Пример тикетов, где мы тестировали:
- https://st.yandex-team.ru/MAPSPRODUCT-1909
- https://st.yandex-team.ru/MAPSPRODUCT-1934
- https://st.yandex-team.ru/MAPSPRODUCT-1937
