# 1. Введение

В данном документе приводится детализированное описание технических решений, которые были применены при построении сети
компании Яндекс. Целью является описание принципов работы сети и типовых конфигураций, систематизация накопленного опыта
и экспертизы.

Целевой аудиторией являются новые сотрудники NOC, дежурные сетевые администраторы и девопсы, которые хотят лучше
понимать работу сети компании.

Принимая во внимание тот факт, что построение используемой на данной момент сети велось с момента создания компании,
в HLD не будут отражены все детали и нюансы legacy-сегментов. Основной фокус будет направлен на описание референсного и
перспективного дизайна сети.

## Скоуп документа

- Описывается целевой дизайн сети ДЦ
- Описываются исключения из целевого дизайна
- Не описывается целевой дизайн и LLD других сетей

## Основные принципы построения сетей ДЦ

- Обеспечение заданных [SLA](https://wiki.yandex-team.ru/users/ilysogor/NOC-SLA/)
- Только IPv6. Внутри ДЦ маршрутизируется только IPv6-трафик. Для передачи IPv4-трафика до конечных серверов используется
  туннелирование "v4 over v6" и NAT64.
- L3 до стоечного коммутатора. Граница маршрутизируемого домена перенесена на стоечные коммутаторы,
  которые выполняют роль "first hop router".
- Только BGP. Единственным протоколом маршрутизации внутри ДЦ является BGP.
- Простота, масштабируемость, отсутствие зависимости от конкретного вендора сетевого оборудования.
- Никакого L2.
- Разделение проектов на уровне адресации и HBF.

## Полезные ссылки

- [История развития сети](https://events.yandex.ru/lib/talks/5895/)
- [Физическое устройство](https://clubs.at.yandex-team.ru/noc/2844)
- [Семинары NOC](https://lms.moe.yandex-team.ru/courses/library/course/19)

## Авторы документа

| Версия    | Автор изменений | Дата       | Что поменялось                |
|:---------:|:---------------:|:----------:|:-----------------------------:|
| v0.1      | Андрей Глазков  | 29.03.2019 | Init                          |
| v0.2      | Андрей Глазков  | 14.06.2019 | Обновил главу с QoS           |
| v0.3      | Андрей Глазков  | 24.06.2019 | Добавил про маршрутизацию во VLA2 и EdgePoD           |
| v0.4      | Иван Лысогор    | 19.08.2020 | Добавление описания подключения серверов           |
