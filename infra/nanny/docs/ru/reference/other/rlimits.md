#  Изменение rlimits

Настройки rlimits, с которыми запускается контейнер, вычисляются следующим образом:

1. Настройки по умолчанию заданы в конфиге iss-agent;
1. **Для сервисов под gencfg** эти настройки (все или только их часть) можно переопределить в UI сервиса в Nanny

    ![rlimits](https://jing.yandex-team.ru/files/sshipkov/2017-09-02_15-13-36.dc84cc0.png)

    ![rlimits](https://jing.yandex-team.ru/files/sshipkov/2017-09-02_15-14-30.e5433fe.png)

1. **Для сервисов под YP-lite** rlimits **уже задраны** на стороне Nanny и силами пользователя их настроить нельзя. Текущие значения вхардкоженные в коде Nanny: `memlock: 549755813888 549755813888; nofile: 102400 1000000;`. Если вам по каким-то причинам не хватает этих значений, пожалуйста, обратитесь в [команду разработки Nanny](https://abc.yandex-team.ru/services/SR).