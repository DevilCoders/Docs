Начиная с версии 8 релизы собираются в New CI:

https://a.yandex-team.ru/projects/mail_frontend/ci/releases/timeline?dir=yandex360%2Ffrontend%2Fservices%2Fmobile-api&id=mobapi-release


## 7.24.0 (19.04.2022)

 * MMAPI-497: Убрать папку для Android клиентов до определенной версии

## 7.23.0 (06.04.2022)

* MMAPI-495: Завести и присылать для папки Reply Later новый тип - 15
* MMAPI-491: Добавить в api/mobile/v1/messages параметр pinned
* MAILSRE-1038: up base image for mobapi
* PSFRONT-217: Перейти с тегов на релизные бранчи
* MMAPI-494: Сборка mobapi в arc

## 7.22.1 (27.03.2022)

MMAPI-494: Сборка mobapi в arc
PSFRONT-232: Перевезти из гита доки web/mobapi

## 7.22.0 (10.03.2022)

* MMAPI-492: Протянуть локаль в ручку фотоподборок
* PSFRONT-208: Улучшить деплой релизных стендов

## 7.21.0 (22.02.2022)

* MMAPI-470: [Filters] Сделать ручку для изменения приоритета правила
* PSFRONT-198: Переключение на новый топик historydb - КОРП, ТЕСТИНГ, duffman
* PSFRONT-193: Обновить базовый контейнер mailfront-base
* PSFRONT-192: Тестовые стенды в деплой (#10252)

## 7.20.0 (Feb 2, 2022)

* MMAPI-488: Пофиксить punycode в v1/settings
* MMAPI-483: Фикс твм datasync
* MMAPI-487: Добавить ctype=client в unistat

## 7.19.0 (Jan 28, 2022)

* MMAPI-483: Протянуть ручку фотоподборок
* PSFRONT-158: Подготовить v1/uaz к возможному новому полю в АБ
* PSFRONT-184: Добавить liveness check для duffman

## 7.18.0 (Jan 16, 2022)

* INFRA: up duffmans
* MMAPI-479: Перейти на protobuf запросы в УАЗ
* MMAPI-479: Удалить неиспользуемый v2/uaz

## 7.17.0 (Jan 14, 2022)

* MMAPI-480: Закешировать translation langs
* MAILAPI-721: Не поднялся push-client
* MAILSRE-950: Поменять в mobapi MCRS на PCRS

## 7.16.0 (Dec 23, 2021)

* PSFRONT-181: Упросить спеку для deploy
* MMAPI-477: up resource

## 7.15.0 (Dec 22, 2021)

* MMAPI-475: handle 413 for v2/translate_message
* MMAPI-474: Актуализировать ошибки авторизации

## 7.14.0 (Nov 15, 2021)

* MMAPI-467: Протащить ручку для статуса восстановления архива писем
* MAILSRE-810: Миграция mobileapi в Deploy

## 7.13.0 (Oct 4, 2021)

* MAILSRE-769: Починить ручку user-apps-activity
* MAILSRE-853: Ночные звонки mobile-api 4xx
* INFRA: update duffman @mobile-api
* INFRA: remove mmapi sonar

## 7.12.2 (Sep 21, 2021)

* MMAPI-464: Оторвать optinEnabled от v2/get_subscription_counters

## 7.12.1 (Sep 15, 2021)

* локаль в конфиге (аффектит абук и капчу)

## 7.12.0 (Sep 15, 2021)

* MMAPI-447: Ручки для фильтров в мобильных
* MMAPI-452: Ручка для кроссаккаунтных запросов поиска по письмам
* MAILSRE-810: Миграция mobileapi в Deploy
* MMAPI-461: Доработать v2/register_domain
* MMAPI-462: Доработки для оптина
* PSFRONT-147: udpate duffman

## 7.11.0 (Aug 25, 2021)

* MMAPI-459: Перейти на использование ручки meta/v2/attach_sid

## 7.10.1 (Aug 24, 2021)

* MMAPI-458: Непрочитанные в табе

## 7.10.0 (Aug 24, 2021)

* MMAPI-439: API для отложенной отправки в мобильных

## 7.9.0 (Aug 19, 2021)

* MMAPI-455: Прокинуть ручку change_register_allowed_ts
* MMAPI-451: Fix limit is not required field
* INFRA: update @yandex-int/express-langdetect
* INFRA: update mail-lib


## 7.8.0 (Aug 18, 2021)

* MMAPI-453: Сломался set_parameters / set_settings
* PSFRONT-143: [mobile-api] update duffman

## 7.7.2 (Aug 10, 2021)

* MAILAPI-677: переделать проверку тарифа в регистрации домена

## 7.7.1 (Aug 10, 2021)

* MAILAPI-677: переделать проверку тарифа в регистрации домена

## 7.7.0 (Aug 10, 2021)

* MMAPI-445: Доработки ручки v2/get_suggested_domains
* MMAPI-434: Доработка API для Красивого адреса в мобильных

## 7.6.0 (Aug 9, 2021)

* MMAPI-443: Непрочитанные в папке
* MMAPI-446: прорастить страну из паспорта в v1/settings
* MMAPI-441: Скрыть папку pending из xlist
* MMAPI-440: Передавать ошибку создания бэкапа на клиент

## 7.5.0 (Jul 15, 2021)

* MMAPI-436: Признак поиска в hidden_trash
* MMAPI-436: Добавить тип для папки Восстанноввленные
* MMAPI-436: Перед созданием бэкапа сохранять настройки папок
* MMAPI-436: Конвертировать tabs и fids
* MMAPI-436: Сохраняем настройку при создании папки hidden_trash
* MMAPI-436: Возвращать hidden_trash_enabled
* MAILSRE-760: lb zstd @ mobile-api
* MMAPI-435: довыпилить миграцию рассылок
* MAILSRE-716: mobile-api access.tskv -> lb

## 7.4.0 (Jun 23, 2021)

* DARIA-69825: remove furita migration guts

## 7.3.0 (Jun 21, 2021)

* MAILSRE-743: https catdog
* MMAPI-431: fix v2/gap
* MMAPI-429: add v2/register_domain method
* MMAPI-429: add v2/cancel_domain_subscription method
* MMAPI-429: add v2/get_suggested_domains method
* MMAPI-429: add v2/get_domain_status method
* DARIA-69775: Завести ручки бэкапа в mobapi
* MAILSRE-718: logbroker tvm @ mobile-api

## 7.2.0 (May 13, 2021)

* MMAPI-427: Добавить сигналов на мульти-инбокс

## 7.1.0 (May 11, 2021)

* MAILAPI-616: Переход на управление рассылками в поиск
* MMAPI-403: Перестать использовать ручку /get_archive_fid
* MMAPI-423: Выпилить старые сиды

## 7.0.0

* MMAPI-424: add mail_b2c_can_use_hidden_trash to v1/settings
* MMAPI-424: add mail_b2c_domain_enable, mail_b2c_can_use_backup to v1/settings
* MAILAPI-638: limit search queries
* PSFRONT-82: mobile-api @ focal
* PSFRONT-107: tune mobile-api rate-limit

## 6.0.0 (Mar 2, 2021)

* MMAPI-421: mobile-api @ nodejs14

## 5.11.0

* INFRA: tune api load
* TRIVIAL: Add AUTH_USER_FROZEN_OR_ARCHIVED error code

## 5.10.0

* MMAPI-414: add v2/create_newsletter_filters method
* MMAPI-414: add v2/trash_messages method
* PSFRONT-96: enable fail-fast for dev duffman start

## 5.9.0

* MMAPI-415: Вырезать необходимые хендлеры из UserSplit (ручка v1/uaz)
* MMAPI-416: Балковая ручка (II)
* MMAPI-416: Балковая ручка (II)
* MAILSRE-475: up duffman @mobile-api
* MMAPI-405: Ручка для балковых запросов моделей
* PSFRONT-93: update tzdata @mobile-api
* MMAPI-411: Добавить код ошибки авторизации отдельным полем
* TRIVIAL: remove deploy to load-amd

## 5.8.0

* MMAPI-406: Добавить признак нужности промотирования Почты 360 в ручку /v1/settings

## 5.7.0
* MMAPI-409: Эксперименты по UUID + FUID
* MMAPI-409: update mial
* TRIVIAL: fix publish docs
* MMAPI-407: Воткнуть костыль для /v2/flags

## 5.6.2

* TRIVIAL: fix build

## 5.6.1

* PSFRONT-86: tune retriever host @ mobile-api
* MAILAPI-586: Mobile-api: Up mial
* MAILAPI-586: Moblie-api: refactor mial errors
* MMAPI-402: Доавить в доку про v2/translate_message параметр novdirect

## 5.6.0 (Oct 26, 2020)

* TRIVIAL: fix missing corp_ava signal
* MMAPI-398: Refactor services config
* MMAPI-397: Исправить типы в v2/flags

## 5.5.0 (Oct 13, 2020)

* MMAPI-395: Стрипать conditions из выдачи, если они были рассчитаны на сервере

## 5.4.1 (Oct 7, 2020)

* MMAPI-386: rename handler

## 5.4.0 (Oct 7, 2020)

* MMAPI-386: fix trust uaas handler
* PSFRONT-64: enable retry budget for mobile-api

## 5.3.0 (Sep 17, 2020)

* MMAPI-389: Add BB tvm id for production
* PSFRONT-63: Update duffmans (retry budgets)
* MMAPI-392: Проверять входные параметры v1/delete_items

## 5.2.0 (Sep 14, 2020)

* MMAPI-388: Оторвать походы в ББ за firstname/lastname
* MMAPI-390: Деградация выдачи get_abook_contact

## 5.1.1 (Sep 11, 2020)

* MMAPI-376: Отвечаем ок для повторной отправки

## 5.1.0 (Sep 10, 2020)

* MMAPI-386: Добавить опцию для траста в v2/flags
* MMAPI-385: Заюзать xmail-flags для расчета кондишнов в v2/flags
* MMAPI-376: Update sbr client

## 5.0.0 (Sep 8, 2020)

* MMAPI-380: Поднять mobile-api на duffman5
* MMAPI-376: Начать ходить за operation_id и пробрасывать его в /send_message

## 4.26.0 (Aug 4, 2020)

* MMAPI-378: Прокинуть в msearch параметр excluded-trash
* MMAPI-374: v1/multi_inbox

## 4.25.0 (Jul 20, 2020)

* MMAPI-375: Add id/list_id to v2/get_abook_contact, v2/get_abook_contacts
* MMAPI-371: Заюзать catdog под капотом v1/ava

## 4.24.0 (Jun 18, 2020)

* MMAPI-364: Abook methods

## 4.23.0 (Jun 5, 2020)

* INFRA: Fix akita params

## 4.22.2 (May 25, 2020)

* MMAPI-368: Исправить проверку telemost_subscriptions

## 4.22.1 (May 25, 2020)

* MMAPI-368: telemost_subscription только для 669 sid

## 4.22.0 (May 22, 2020)

* MMAPI-368: Прокинуть атрибут telemost_subscription в ручку settings
* MMAPI-367: Add events to v2/get_abook_contact

## 4.21.1 (May 12, 2020)

* MMAPI-365: Добавить v1/message_text

## 4.20.0 (Apr 15, 2020)

* MMAPI-362: Добавить mobile:yes в поход за виджетами
* MMAPI-361: Подробнее про limited в v1/send

## 4.19.2 (Mar 26, 2020)

* Add connectionId fallback for v1/store, v1/send

## 4.19.1 (Mar 25, 2020)

* MOBILEMAIL-16597: [AMP] Не открываются ссылки внутри формы

## 4.19.0 (Mar 20, 2020)
* Добавил апи для амп-форм для мобильных приложений

## 4.18.4 (Mar 19, 2020)

* MMAPI-354: Фильтровать vcard для некорповых шареных контактов

## 4.18.3 (Mar 16, 2020)

* MMAPI-357: Значения rotate из параметров игнорируется по флагу бункера

## 4.18.2 (Mar 16, 2020)

* MMAPI-357: Значения rotate и langs параметров в ручке фотописем

## 4.18.1 (Mar 12, 2020)

* MMAPI-356: Add side param to msearch calls

## 4.18.0 (Mar 12, 2020)

* MMAPI-353: Прокинуть параметр adv_search вместо query-language в msearch
* MMAPI-354: Исправить проверку staff-affiliation
* MMAPI-352: Update schema for v1/search

## 4.17.0 (Mar 4, 2020)

* Add v1/search params (hdr_subject, hdr_to_cc_bcc)
* MMAPI-349: Перестать отдавать персональные данные внешним сотрудникам

## 4.16.0 (Feb 26, 2020)

* MMAPI-345: Убрать походы в ручку colllie location
* MMAPI-346: Отпилить неиспользуемый v2/search_contacts
* MMAPI-344: Отпилить duffman-mail-services
* INFRA: Remove graphite duffman log parsers

## 4.15.0 (Feb 21, 2020)

* INFRA: Fix v1/message_header widgets
* MMAPI-342: Ходить в календарь с tvm
* MMAPI-329: Ручка для фотописем
* MMAPI-328: Ручка для Office Lense
* MMAPI-339: Update duffman 3.9.2

## 4.14.0 (Feb 19, 2020)

* MMAPI-339: Update duffman (deadline propagation)
* TRIVIAL: Исправить определение ics аттача для v2/save_event

## 4.13.0 (Feb 11, 2020)

* MMAPI-331: Ходим в таксу с TVM2
* MMAPI-330: Доработали запрос и выдачу календарных виджетов
* MMAPI-332: Пробросили клиентами настройку биллинга для отключения рекламы
* MMAPI-333: Защищенные настройки

## 4.12.0 (Feb 7, 2020)

* MMAPI-315: Поменялся формат ответа uaz ручек
* MMAPI-330: Доработана ручка календарных виджетов (отфильтрованы controls, синхронные поход в таксу)
* Добавлено описание параметра system для v1/message_body

## 4.11.0 (Feb 3, 2020)

* MMAPI-317: Проксирование ручки календаря
* Добавлен параметр mdb для таксы
* Добавлен скрипт deploy-canary

## 4.10.0 (Jan 30, 2020)

* MMAPI-315: Протащили в ответ ручки uaz правильные идентификации эксперимента (тройки)
* Исправлена схема ответа v1/set_parameters

## 4.9.0 (Jan 27, 2020)

* MMAPI-323: Добавились методы генерации/проверки капчи
* MMAPI-320, MMAPI-288: Выпилены из выдачи настроек подписи
* MMAPI-321: Разобрались с ретраями в sbr

## 4.8.0 (Jan 20, 2020)

* MMAPI-312: TVM2 для диска
* MMAPI-316: Исправлен mops при tvm-авториазции
* MMAPI-313: Убран tvm1 из запросов
* MMAPI-314: Исправлен v1/message_body со смарт-реплаями

## 4.7.1 (Jan 10, 2020)

* MMAPI-297: Исправлена ручка для адресной книги

## 4.7.0 (Jan 9, 2020)

* MMAPI-309: Добавлены календарные виджеты
* MMAPI-297: Исправлена ручка для адресной книги

## 4.6.0 (Dec 17, 2019)

* MMAPI-305: В v1/message_body добавлег признак показывать Quick Reply или нет
* MMAPI-307: TVM авторизация для бэкенда Алисы
* MMAPI-303: В v1/message_body добавлены смарт реплаи

## 4.5.0 (Dec 4, 2019)

* MMAPI-299: Flags.json handler
* MMAPI-301: Запроксировать gap

## 4.4.0 (Dec 2, 2019)

* MMAPI-296: Промокоды для диска

## 4.3.0 (Nov 28, 2019)

* MMAPI-295: Удалить compose-check
* MMAPI-298: Поддержать возможность получения guid для корпов

## 4.2.0 (Nov 22, 2019)

* MMAPI-283: В v2/get_abook_contact добавлены organizations
* MMAPI-294: Добавлен метод v2/send_limits
* MMAPI-282: Поддержана капча в v1/send
* MMAPI-291: Заюзан новый ckey
* MMAPI-289: Исправлен v2/save_event

## 4.1.1 (Nov 21, 2019)

* MMAPI-289: Fix calendar request

## 4.1.0 (Nov 20, 2019)

* MMAPI-283: Добавлен метод v2/get_abook_contact
* MMAPI-285: Фикс TVM-авторизации

## 4.0.0 (Nov 15, 2019)

* MMAPI-285: TVM-авторизация для v1/xlist, v1/messages
* MMAPI-286: Фильтрация эльфийского в v2/translation_langs

## 3.27.0 (Nov 11, 2019)

* MMAPI-280: Расширены параметры похода в mlp
* MMAPI-279: Автовыкатка ресурса на стенд

## 3.26.0 (Nov 1, 2019)

* MMAPI-276: Методы для работы с приглашениями в календарь
* MMAPI-277: Добавлен original_lang в ответе v2/translate_message
* MMAPI-272: Добавлена ручка для получения id чата мессенджера
* MMAPI-275: Запуск корпового mobile-api в qyp

## 3.25.0 (Oct 22, 2019)

* MMAPI-273: Исправлен язык в v2/translate_message
* MMAPI-270: Ограничен максимальный размер дисвового аттача в ответе
* MMAPI-271: Исправлены скрытые параметры в логгировании send/store

## 3.24.1 (Oct 22, 2019)

* MMAPI-268: Удалены проверка заголовка x-yandex-mdbidver и статус NEED_RESET

## 3.23.0 (Oct 15, 2019)

* MMAPI-266: Деплой ресурсами
* MMAPI-259: Улучшен поиск по табам

## 3.22.0 (Oct 11, 2019)

* MMAPI-263: Поддержка автоопределения исходного языка при переводе
* MMAPI-253: Исправлен перевод text/plain писем
* MMAPI-196: Исправлен `subjEmpty` для различных локалей
* MMAPI-243: Забетонирован эксперимент collie
* MMAPI-264: Отправка в mlp полного текста письма
* MMAPI-259: Поиск по табам

## 3.21.0 (Sep 26, 2019)

* MMAPI-261: Параметр novdirect для v1/message_body принимает boolean

## 3.20.0 (Sep 26, 2019)

* MMAPI-257: Новый базовый докер-образ
* Улучшен watchdog duffman

## 3.19.0 (Sep 16, 2019)

* MMAPI-256: Добавлено событие по обновлению счетчиков в папке (v2/changes)

## 3.18.0 (Sep 9, 2019)

* MMAPI-249: Добавлен параметр для ограничения длины ответов /v2/quick_reply_suggestions
* Тюнинг сборки
* Обновлен mail-lib
* Добавлен CHANGELOG.md

## 3.17.0 (Sep 2, 2019)

* MMAPI-248 поддрержка режима табов в v2/changes
* переезд в новый репозиторий

## 3.16.0 (Aug 30, 2019)

* Ускорена сборка
* Изменен формат логов duffman
* Изменен парсер логов для графита
* Обновления для разработки в QYP
* Обновлен readme
* MMAPI-240: Забетонирован новый sendbernar

## 3.15.2 (Aug 30, 2019)

* Конфиг aceventura

## 3.15.1 (Aug 16, 2019)

* MMAPI-242: Новый абук, исправлены ответы

## 3.15.0 (Aug 16, 2019)

* MMAPI-242: Новый абук под экспериментом

## 3.14.1 (Aug 5, 2019)

* MMAPI-233: Fix sendbernar

## 3.14.0 (Aug 5, 2019)

* MMAPI-233: Новая библиотека sendbernar'а под экспериментом

## 3.13.0 (Aug 2, 2019)

* MMAPI-234: Поддержан новый api для дисковых аттачей sendbernar'а

## 3.12.1 (Aug 1, 2019)

* Исправлена сборка докер-образа

## 3.12.0 (Aug 1, 2019)

* tvm для msearch

## 3.11.1 (Aug 1, 2019)

* MMAPI-236: Включен tvm для mlp

## 3.11.0 (Aug 1, 2019)

* MMAPI-236: Добавлен метод v2/quick_reply_suggestions
* Исправлен док v1/push

## 3.10.0 (Jul 22, 2019)

* MMAPI-232: Новый режим работы v2/changes
* MMAPI-231: Включена авторизация для center-api

## 3.9.2 (Jul 15, 2019)

* Исправлены сигналы для графита

## 3.9.1 (Jul 15, 2019)

* Исправлены сигналы для графита

## 3.9.0 (Jul 15, 2019)

* Исправлена документация v2/translation_langs
* MMAPI-228: Добавлен метод v2/search_suggest_remove

## 3.8.0 (Jun 25, 2019)

* MMAPI-221: Добавлен lang в v1/message_body
* MMAPI-225: Исправлена обратная совместимость v2/get_tab_counters
* MMAPI-222: Исправлена обработка ошибок от хаунда

## 3.7.0 (Jun 18, 2019)

* MMAPI-217: Проброс extra в push api
* MMAPI-219: Pkpasses в ответе message_body
* MMAPI-220: Исправлен v1/move_to_folder для работы с табами

## 3.6.0 (Jun 18, 2019)

* MMAPI-209: Добавлены методы для перевода

## 3.5.0 (Jun 12, 2019)

* MMAPI-177: Проброс хэша аттачей в v1/upload, v1/store
* MMAPI-215: Обратная совместимость табов

## 3.4.0 (Jun 6, 2019)

* MMAPI-214: Пробрасываем дополнительные параметры в поиск

## 3.3.1 (Jun 4, 2019)

* MMAPI-213: Исправлено перемещение в таб

## 3.3.0 (Jun 4, 2019)

* MMAPI-208: Виджеты в messages-подобных ручках
* Добавлены make-рецепты для докера

## 3.2.1 (May 28, 2019)

* MMAPI-211: Доработки табов

## 3.2.0 (May 28, 2019)

* MMAPI-193: Включили TVM2

## 3.1.2 (May 20, 2019)

* MMAPI-203: Поддержка табов в v1/push
* Обновление зависимостей
* Duffman 3.1.0

## 3.1.1 (May 6, 2019)

* MMAPI-204: Увеличен дефолтный таймаут в msearch
* Обновлены зависимости

## 3.1.0 (May 5, 2019)

* MMAPI-201: Добавлен uid в duffman access log
* MMAPI-199: Добавлена поддержка табов

## 3.0.15 (May 5, 2019)

* MMAPI-188: Добавлены сигналы в голован

## 3.0.14 (May 5, 2019)

* MAILAPI-120: Добавлена документация в формате OpenAPI

## 3.0.13 (Apr 12, 2019)

* MMAPI-154: Поддержаны изменения в ручке /change_tab мопса

## 3.0.12 (Apr 9, 2019)

* MMAPI-191: обновлен duffman, включен fail-fast

## 3.0.11 (Apr 9, 2019)

* MMAPI-184: исправлены сигналы по ошибкам методов v2

## 3.0.10 (Apr 9, 2019)

* MMAPI-184: исправлены сигналы по ошибкам методов v2

## 3.0.9 (Apr 9, 2019)

* MMAPI-181: добавлен метод v1/reset_unvisited
* MMAPI-181: добавлен флаг unvisited в папки в v1/xlist
* MMAPI-183: увеличен таймаут котопса до 1 сек
* MMAPI-180: автовыкладка на корповый qa

## 3.0.8 (Mar 1, 2019)

* MOBILEMAIL-13404: Проброс в ксиву версии ios

## 3.0.7 (Mar 1, 2019)

* Исправлены сигналы в головане
* MMAPI-178: Испраления v1/corp_ava

## 3.0.6 (Feb 23, 2019)

* MMAPI-12: Обновились хосты бэкендов
* MMAPI-153: Автоматическое разворачивание в QA
* MMAPI-172: Фикс с инлайновыми xls

## 3.0.5 (Feb 5, 2019)

* MMAPI-170: Графики в головане по каждому методу

## 3.0.4 (Feb 1, 2019)

* MAILPG-2304: Конфиг nginx

## 3.0.3 (Feb 1, 2019)

* MMAPI-176: Добавился проброс параметра system в бэкенд mbody

## 3.0.2 (Jan 29, 2019)

* MMAPI-174: Исправлены коды ответов v2/changes, v3/diffset при неправильном запросе

## 3.0.1 (Jan 28, 2019)

* MMAPI-12: Ходим в akita, mops, mbody, sendbernar по https

## 3.0.0 (Jan 17, 2019)

* Добавился экспериментальный v3/exec

## 2.8.18 (Jan 9, 2019)

* MMAPI-169: Исправлены параметры похода в mbody для v2/disk_save, v2/disk_save_all

## 2.8.17 (Dec 21, 2018)

* Добавлен rate limit для production

## 2.8.16 (Dec 20, 2018)

* Исправлены права в /etc/logrotate.d, /etc/cron.d

## 2.8.15 (Dec 20, 2018)

* Исправлен формат ответа v1/xlist при недоступности/ошибке meta

## 2.8.14 (Dec 19, 2018)

* Исправлены ответы в v2 при недоступности акиты

## 2.8.13 (Dec 13, 2018)

* MMAPI-163: Исправлены 500 в v1/with_attachments, v1/only_new

## 2.8.12 (Dec 13, 2018)

* MMAPI-159: Исправлено сохранение на диск
* MMAPI-160: Уведомления в ST о сборке образов
* MMAPI-161: Удалены старые ключи

## 2.8.11 (Dec 13, 2018)

* MMAPI-157: Исправлено сохранение на диск

## 2.8.10 (Nov 28, 2018)

* MMAPI-157: Исправлена ошибка сохранения на диск всех аттачей

## 2.8.9 (Nov 28, 2018)

* MOBILEMAIL-12622: Исправили ответ апи при пустом from
* Покрытие для sonar считается в trendbox
* MMAPI-152: Настройки для load

## 2.8.8 (Nov 13, 2018)

* Исправлены сигналы статсервера

## 2.8.7 (Nov 11, 2018)

* MMAPI-152: Добавились настройки для стрельб #99

## 2.8.6 (Nov 8, 2018)

* Nginx unistat

## 2.8.5 (Nov 1, 2018)

* MMAPI-148: v2/classification переведен на POST, midы в логах маскируются
* фиксы деплоя #95 , обработки ошибок #96

## 2.8.4 (Nov 1, 2018)

* async/await
* QUINN-6010: подключили ревьюшницу

## 2.8.3 (Oct 23, 2018)

* MMAPI-150: Увеличен таймаут до бэкенда v2/classification
* MMAPI-151: Сборка в trendbox

## 2.8.2 (Oct 16, 2018)

* MMAPI-145: Добавлены проверки при сборке

## 2.8.1 (Oct 16, 2018)

* MMAPI-143: Добавлен параметр fid в v2/purge_items
* MMAPI-144: Добавлен v2/versions

## 2.8.0 (Oct 16, 2018)

* Заменили co в AbstractRouter на async/await

## 2.7.2 (Oct 16, 2018)

* MMAPI-141: Отпилен yarn — больше не используется

## 2.7.1 (Oct 5, 2018)

* MMAPI-140: Включена группировка контактов в v1/abook_top

## 2.6.5 (Oct 1, 2018)

* MMAPI-138: Отпилены зависимости p2p-distribution и libgeobase

## 2.6.0 (Sep 28, 2018)

* MMAPI-138: Вернулась обвязка для сборки deb

## 2.5.4 (Sep 19, 2018)

* Изменения настроек таймаутов akita

## 2.5.3 (Sep 12, 2018)

* MMAPI-134: Увеличены таймауты при походе за саджестом (v2/search_suggest)
* MMAPI-134: Проброс параметра timeout (v2/search_suggest)

## 2.5.2 (Sep 12, 2018)

* MMAPI-133: Исправлены ответы API при http ошибках на бэкендах

## 2.5.1 (Sep 7, 2018)

* MMAPI-132: Табы в мете по письмам

## 2.5.0 (Sep 6, 2018)

* MMAPI-120: Добавлен mailbox_revision в v1/xlist
* MMAPI-120: Добавлен метод v2/changes

## 2.4.20 (Sep 6, 2018)

* MMAPI-131: Не стартовать супервизор без секретов

## 2.4.19 (Sep 6, 2018)

* Настройки образа

## 2.4.18 (Sep 6, 2018)

* Настройки образа

## 2.4.17 (Sep 6, 2018)

* MMAPI-113: Обновлены duffman-services

## 2.4.16 (Sep 3, 2018)

* MMAPI-113: Запроксирована ручка Ксивы apns_queue_repeat (v2/apns_queue_repeat)

## 2.4.15 (Sep 3, 2018)

* Исправлена схема запроса сообщений

## 2.4.14 (Aug 31, 2018)

* MMAPI-130: Добавление системных папок по символу
* Исправлена схема запроса сообщений

## 2.4.13 (Aug 31, 2018)

* MMAPI-52: Исправлен запрос в диск (сохранение аттачей)

## 2.4.12 (Aug 31, 2018)

* MMAPI-129: Добавлен v2/get_newsletters

## 2.4.11 (Aug 30, 2018)

* MMAPI-124: Исправлена ошибка с тредами по табам

## 2.4.10 (Aug 30, 2018)

* Сборка в docker

## 2.4.9 (Aug 30, 2018)

* MMAPI-121: Исправлена проверка параметров v2/get_tab_counters
* Обновлен duffman
* Сборка в docker

## 2.4.8 (Aug 30, 2018)

* MMAPI-124: Добавлен параметр tab для смены таба после переноса в папку и схема запроса

## 2.4.7 (Aug 23, 2018)

* MMAPI-122: Обновлены правила подписки на пуши

## 2.4.6 (Aug 23, 2018)

* MMAPI-122: Добавлен параметр exclude_tabs в ручку подписки на пуши

## 2.4.5 (Aug 23, 2018)

* MMAPI-121: Исправлен метод в v1/messages для табов, когда указан fid

## 2.4.4 (Aug 23, 2018)

* QUINN-5817: Исправлен v2/classification (походы в бэкенды, валидация параметров)

## 2.4.3 (Aug 23, 2018)

* QUINN-5817: Добавлена схема запроса к v2/classification

## 2.4.2 (Aug 23, 2018)

* MMAPI-101: Исправлены инлайнонвые pdf

## 2.4.1 (Aug 16, 2018)

* MMAPI-52: Заюзана новая ручка сохранения почтовых аттачей на диск

## 2.4.0 (Aug 16, 2018)

* MMAPI-121: Добавлены методы и параметры для работы с табами

## 2.3.4 (Aug 8, 2018)

* QUINN-5817: Добавлен метод v2/classification
* MMAPI-117: Добавлены recipients в ответы messages-подобных ручек
* MMAPI-101: Все pdf-аттачи считаются неинлайновыми

## 2.3.3 (Jul 27, 2018)

* MMAPI-115: Пробрасываем параметр reqid для v1/search

## 2.3.2 (Jul 24, 2018)

* MMAPI-114: Исправлено имя файла при сохранении на диск

## 2.3.1 (Jul 10, 2018)

* MMAPI-107: В саджест добавлены id

## 2.3.0 (Jul 9, 2018)

* MMAPI-105: Добавлен v2/search_contacts
* MMAPI-106: Опциональная выдача html-highlight'ов в v2/search_suggest, v2/search_contacts

## 2.2.1 (Jul 9, 2018)

* MMAPI-67: Запросы дисковых аттачей из mbody в message-подобных методах v1

## 2.2.0 (Jun 28, 2018)

* MMAPI-67: В messages-подобные ручки добавлена инфа по аттачам.
* MMAPI-100: Добавлен фоллбек reqid в v2/search_suggest

## 2.1.5 (Jun 28, 2018)

* MMAPI-98: Исправлено взаимодействие с ручкой сохранения поиска

## 2.1.4 (Jun 20, 2018)

* MMAPI-91: v2/search_suggest: использовать обычный поиск по-умолчанию
* MMAPI-92: Прокинут conection_id из ответа ЧЯ в ксиву
* MMAPI-93: Тело успешного ответа модифицирующих операций теперь {}
* MMAPI-97: Исправлены пометки писем при ответе / пересылке
* MMAPI-98: Добавлен метод v2/search_save
* MMAPI-98: Добавлен опциональный параметр dont_save для v1/search

## 2.1.3 (May 22, 2018)

* MMAPI-86: Исправлен v2/search_suggest

## 2.1.2 (May 6, 2018)

* MMAPI-70: Исправлено сохранение/отправка писем из шаблонов

## 2.1.1 (May 4, 2018)

* MMAPI-82: Изменен формат выдачи v2/search_suggest

## 2.1.0 (Apr 25, 2018)

* MMAPI-63: Исправлено сохранение на диск по коротким ссылкам
* MMAPI-72: Обработка ошибок авторизации
* MMAPI-78: Размер дисковых аттачей приведен к числу
* MMAPI-79: Изменен формат ответа для дисковых аттачей (class: 'folder' и другие классы)
* MMAPI-80: Настроен кондуктор

## 2.0.6 (Apr 20, 2018)

* MMAPI-73: Добавилось логирование project=MOBILE-API в http-лог

## 2.0.5 (Apr 20, 2018)

* MMAPI-71: Прокидываем user-agent из запроса в бэкенды

## 2.0.4 (Apr 5, 2018)

* Слились с 1й версией
* Откатили MMAPI-61 (порт воркера в даффмен-логах)

## 1.3.15 (Apr 2, 2018)

* MMAPI-61: В логи добавлен порт даффмен-воркера

## 1.3.14 (Mar 29, 2018)

* MMAPI-60: Исправлен ответ при разавторизации ряда методов

## 1.3.13 (Mar 29, 2018)

* MMAPI-59: Улучшено отображение ошибок sendbernar

## 1.3.12 (Mar 29, 2018)

* MMAPI-57: Исправлен баг с пустым scn

## 1.3.11 (Mar 27, 2018)

* MMAPI-54: Исправлены параметры запросов в мету
* MMAPI-55: Исправлен формат scn в v1/messages
* MMAPI-56: Исправлена тротлилка запросов в мету в v1/messages

## 1.3.10 (Mar 23, 2018)

* MMAPI-53: Изменена ручка под капотом v1/vdirect

## 1.3.9 (Mar 19, 2018)

* MMAPI-50: Расширена парсилка версий
* MMAPI-51: Исправлены ответы при неуспешной авторизации v1/xlist, v1/messages

## 1.3.8 (Mar 14, 2018)

* MMAPI-49: В iOS вернулась поддержка типа папок unsubscribe

## 1.3.7 (Mar 13, 2018)

* MMAPI-48: Повторили кастомный reply_to в настройках из старого апи

## 1.3.6 (Mar 12, 2018)

* MMAPI-46: Исправлен формат ответа facts в v1/message_body

## 1.3.5 (Mar 12, 2018)

* MMAPI-45: Немного разтормозили тормозилку в мету

## 1.3.4 (Mar 12, 2018)

* MMAPI-42: Исправлен ошибочный кейс в v1/message_body

## 1.3.3 (Mar 5, 2018)

* MMAPI-38: Подтюнили тип "отписок" для старых версий

## 1.3.2 (Mar 2, 2018)

* MMAPI-27, MMAPI-36: Исправлен статус в access log в ответе /v1/messages

## 1.3.1 (Feb 27, 2018)

* MMAPI-36: В access-log добавлен статус ответа апи
* MMAPI-33: Удален старый роут

## 1.3.0 (Feb 21, 2018)

* MMAPI-33: Роут заменен на /mobileapi, старый (/api/mobile) временно сохранен
* MMAPI-30: Исправлен тип для папки "скрытые рассылки"
* MMAPI-27: Передача статуса ошибки через заголовок

## 1.2.9 (Feb 21, 2018)

* MMAPI-26: Подзакручена тротлилка запросов в hound

## 1.2.8 (Feb 21, 2018)

* MMAPI-23: Исправлены class и preview_support в методе /store

## 1.2.7 (Feb 21, 2018)

* MMAPI-18: Исправлен ответ xlist

## 1.2.6 (Feb 21, 2018)

* Исправлен путь до аттачей в корпе

## 1.2.5 (Feb 21, 2018)

* MOBILEMAIL-10748: Добавлены расширения .eml для соответствующих вложений
* Исправлен mime-type аттачей в ответах message_body
* Исправлен uaz
