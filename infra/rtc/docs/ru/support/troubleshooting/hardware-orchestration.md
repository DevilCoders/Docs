# Вопросы о работе wall-e/hwatcher/cms
## Таймаут на missing-чеки {#walle-missing}
В случае, если проверки Unreacable & SSH проходят, но при этом остальные пассивные чеки находятся в состоянии **missing**, Wall-e запустит цепочку починки Reboot -> Profile -> Deploy спустя сутки после перехода чеков в состояние **missing**, [RTCSUPPORT-5008](https://st.yandex-team.ru/RTCSUPPORT-5008#5dd273081221545ac4ad2367).
