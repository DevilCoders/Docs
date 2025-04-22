## Как настроить ассессорскую прокси
Окружение прокси - [disk-assessors](https://platform.yandex-team.ru/projects/disk/disk-assessors/stable)

1. в /etc/hosts настроить хосты на нужные адреса (актуальные ip можно посмотреть в qloud)
#accessors
213.180.193.96 disk.yandex.ru
2a02:6b8::1:96 disk.yandex.ru
213.180.193.96 yadi.sk
2a02:6b8::1:96 yadi.sk

2. добавить куку host=N N - номер престейбла, на который нужно настроиться
   для этого - зайти на disk.yandex.ru?host=N

3. авторизоваться на yandex-team.ru

4. дальше ходить на продовские урлы
