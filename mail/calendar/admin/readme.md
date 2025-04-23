## Страница Админки Календаря:

### UI:
#### Public:
https://admin.calendar-public.yandex-team.ru

https://calendar-public-testing.common.yandex.net/admin

#### Corp:
https://admin.calendar-yt.yandex-team.ru

https://calendar-yt-testing.common.yandex.net/admin

[Сборка в sandbox](https://sandbox.yandex-team.ru/task/1290016608)


Сборка руками:
```ya package package.json --docker-network=host --docker --docker-repository=mail/calendar --docker-push [--custom-version <указать версию руками>]```
