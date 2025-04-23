# Заметки об Unbound

На этой странице собраны некоторые знания о сервере.

## Основные ссылки

Сайт проекта: <https://nlnetlabs.nl/projects/unbound/about/>.

Наиболее важные страницы:

- Страница с релизами: <https://nlnetlabs.nl/projects/unbound/download/>
- Документация: <https://unbound.docs.nlnetlabs.nl/en/latest/>
  - Документация к конфигу Unbound: <https://unbound.docs.nlnetlabs.nl/en/latest/manpages/unbound.conf.html>
  - Сгенерированная по коду документация: <https://www.nlnetlabs.nl/documentation/unbound/doxygen/index.html>

Также можно подписаться на [почтовую рассылку](https://lists.nlnetlabs.nl/mailman/listinfo/unbound-users), чтобы следить за новыми релизами и за обсуждениями комьюнити.

Open-source разработка ведется в ГитХабе: <https://github.com/NLnetLabs/unbound>.
В [Issues](https://github.com/NLnetLabs/unbound/issues) можно задать вопрос или зарепортить о проблеме и получить ответ от разработчиков.

## Код

Оригинальный код находится в ГитХабе: <https://github.com/NLnetLabs/unbound>.
Релизы оттуда [импортируются](../unbound/arcadia.md) в Аркадию в [contrib/tools/unbound](https://a.yandex-team.ru/arcadia/contrib/tools/unbound) и дополнительно туда накладываются патчи специфичные для Яндекса.

### Обзор структуры репозитория

- `.yandex_meta` - какие-то данные про лицензии, которые пишет license analyzer от yamaker [\[1\]](https://clubs.at.yandex-team.ru/arcadia/26540)[\[2\]](https://clubs.at.yandex-team.ru/arcadia/25149)
- `/build/scripts` - в директории лежат скрипты, используемые для сборки Unbound через Ya Make в Аркадии
- `/compat` - реализации каких-то стандартных функций, которых по каким-то причинам нет в Аркадии или они просто не нашлись
- `/daemon` - входная точка для чтения кода непосредственно сервера
  - `/daemon/unbound.c` - тут функция `main`
  - `/daemon/daemon.{h,c}` - код демона, читает конфиг, все иницилизирует, запускает воркеры, которые обслуживают запросы
  - `/daemon/worker.{h,c}` - код воркера, обрабатывающего запросы; один тред - один воркер; основная функция `worker_handle_request`
- `/dns64`, `/dnscrypt`, `/dnstap`, `/edns-subnet` - код, который реализуют поддержку данных технологий (о них можно нагуглить) в Unbound
- `/iterator` - модуль, который выполняет рекурсивную итеративную обработку DNS-запросов
- `/libunbound` - <https://unbound.docs.nlnetlabs.nl/en/latest/manpages/libunbound.html>
- `/limiters` - здесь код, разных лимитеров запросов; на данный момент там один `project_id_outbound_limiter` ([TRAFFIC-12124](https://st.yandex-team.ru/TRAFFIC-12124))
- `/services` - реализации разных примочек-фичей Unbound
  - `/services/authzone.{h,c}` - код, отвечающий за работу с авторитетными зонами; туда непосредственно внедрен код, использующий модуль YP DNS
  - `/services/outside_network.{h,c}` - отправка запросов во внешние авторитеты, ожидание их ответов
  - остальное можно сматчить с [документацией](https://unbound.docs.nlnetlabs.nl/en/latest/manpages/unbound.conf.html) к конфигу или почитать комменты сверху в коде, там есть краткое описание
- `/sldns` - константы, парсинг, конвертация форматов и другое всякое полезное для общего кода
- `/smallapp` - код утилит unbound-X; документация к X [здесь](https://unbound.docs.nlnetlabs.nl/en/latest/manpages/unbound-checkconf.html) в секции Manual Pages
- `/unbound`, `/unbound-X` - директории с ya.make файлами для сборки программ через Ya Make
- `/util` - разный полезный и слабосвязанный код
- `/yp_dns` - код-прослойка между нативным кодом Unbound и плюсовой либой [infra/libs/unbound](http://a.yandex-team.ru/arcadia/infra/libs/unbound)
- `config.h` - разные дефайны

Все, что не описано, либо не столь важно, либо неизвестно что это.
В принципе, в каждом `.h` файле в комментарии есть краткое описание о чем этот код.
