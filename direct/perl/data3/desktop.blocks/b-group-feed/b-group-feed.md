r107790
## b-group-feed ##
Блок выбора фида для группы смарт-баннеров и ДО
Используется на странице мультиредактирования смарт-баннеров/ДО

Выглядит [вот так](http://jing.yandex-team.ru/files/alkaline/2015-09-18_1822.png)

## Пример ##
    {
        block: 'b-group-feed',
        mix: { block: 'b-edit-group', elem: 'feed' },
        selectedFeedId: this.group.feed_id,
        feeds: this.feeds,
        disabled: this.group.feed_id != 0
    }
