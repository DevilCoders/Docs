# Привязать или переместить облако клиента к партнерскому саб-аккаунту

В этом разделе вы узнаете как привязать облако к саб-аккаунту партнера и как переместить его в аккаунт клиента.

## Привязать облако {#bind}

Привязать облако клиента к партнерскому саб-аккаунту можно из консоли партнера и из консоли клиента.

{% list tabs %}

- Консоль партнера

    1. Перейдите на вкладку **Биллинг**, выберите аккаунт клиента и войдите в него.
       <скриншот вкладки **Биллинг** со списком аккаунтов>
    1. Нажмите кнопку **Привязать облако**. 
    1. Выберите необходимое облако из выпадающего списка. Нужное облако может отсутствовать в списке, если:
       * прошло слишком мало времени с момента выдачи роли партнеру в консоли клиента;
       * требуется сменить роль на это облако.


- Консоль клиента

    Чтобы в консоли клиента переместить облако из аккаунта клиента в саб-аккаунт партнера: 
    1. Нажмите на значок ![image](../../_assets/options.svg) в саб-аккаунте партнера.
    1. Выберите **Привязать облако**.
    1. Выберите облако, которое следует привязать.
    
    Чтобы партнер не смог самостоятельно привязать облако клиента, необходимо забрать у партнера роли на ресурсы. Узнайте подробнее о [ролях в {{ yandex-cloud }}](../../resource-manager/security/).

{% endlist %}

## Перемещение облака {#move}

{% list tabs %}

- Консоль клиента

    Чтобы переместить облако из саб-аккаунта партнера в аккаунт клиента:
    1. В консоли клиента в своем аккаунте нажмите значок ![image](../../_assets/options.svg).
    1. Выберите **Привязать облако**.
    1. Выберите облако, которое нужно переместить в свой аккаунт.

{% endlist %}