#i-mass-action-metrika-counter
Блок для изменения счетчиков метрики в массовых действиях над кампаниями.
Используется в b-mass-actions_type_camps.js

##Пример использования
metrikaManager = BEM.create('i-mass-action-metrika-counters', {
    affectedCids: affectedCids,
    performanceCount: performanceCount,
    defaultCounter: this.params.metrikaCounters
});
metrikaManager.on('close', function() {
    metrikaManager.destruct();
}, this);

metrikaManager.openPopup();

Принимает список измененных cid-ов, количество смарт-кампаний среди выбранных и дефолтный счетчик метрики на аккаунт.
После закрытия попапа кидает событие metrikaChanged
Умеет
1) открывать попап счетчиков метрики,
2) делать проверки-простукивания счетчиков,
3) дергает java-ручки на добавление, замену, удаление счетчиков
4) показывает ошибки, которые возвращает ручка
5) умеет показывать предупреждения о смарт-кампаниях (у них всегда строго 1 счетчик)

##Мейнтейнеры
[anyakey](staff.yandex-team.ru/anyakey)
