Вы хотите добавить новые сообщения/поля в .proto и, потенциально, они могут понадобиться мобильным клиентам. Это предполагает следующий набор задач:

1. **Пройти ревью на изменение протокола (сами .proto-файлы).** В общем случае, ревью должно содержать в себе примеры (папка `examples`) и тесты, которые эти примеры генерируют. Это ревью должен обязательно шипнуть [Виктор Теплов][grok]. Не рекомендуется писать какой-либо production-код до прохождения этого этапа, потому что в процессе ревью может измениться постановка задачи.
2. **Написать код, который будет генерировать новые данные.** Это может быть новый сниппет, изменения в геопоиске или Справочнике, etc. После прохождения этого этапа у вас должна быть возможность получить новые данные из сервиса. _Все пункты дальше нужны только, если новые данные нужны мобильным клиентам._
3. **Добавить в MapKit [построение IDL][idl] из .proto.** IDL позволяет использовать данные из ответа мобильным клиентам. Ревью на добавление должен шипнуть кто-то из списка owner-ов IDL.
4. **Добавить в MapKit возможность запросить эти данные.** Если вы расширяете существующие сообщения, то обычно это не нужно. Но если вы добавляете новый [сниппет][snippet] или новый [endpoint][endpoint], то это требует доработок со стороны MapKit. Обычно тоже предполагает изменение IDL.
5. **Поддержать новый endpoint в [мобильной прокси][proxy].** Нужно только для новых endpoint-ов.
6. **[Android] Поддержать новый IDL в [TestApp для Android][test_app_android].** Это позволит в будущем быстро проверять, что новые данные доходят до мобильных клиентов. Здесь обычно правильно отдавать задачу на ручное тестирование кому:adavidenko, чтобы тестировщики узнали про существование новых данных, проверили, что они ожидаемо работают на разных устройствах, и при необходимости завели тесткейсы.
7. **[Android] Поддержать новые данные в [автотестах][android_tests].** Если есть возможность написать автотест на новые данные, то лучше так и сделать. Так их доставка будет автоматически проверяться каждый релиз MapKit, и тестировщикам не придётся для этого делать ничего руками.
8. **[iOS] Поддержать новый IDL в [TestApp для iOS][test_app_ios].** Аналогично. Задачу можно делать независимо от Android.
9. **[iOS] Поддержать новые данные в [автотестах][ios_tests].** Аналогично. Задачу можно делать независимо от Android.

Примеры задач на расширение протокола:
* [бронирование][booking] с новым endpoint-ом
* [модульный сниппет][modular]

[grok]: https://staff.yandex-team.ru/grok
[idl]: https://a.yandex-team.ru/arc/trunk/arcadia/maps/mobile/libs/search/response/idl/search
[snippet]: https://a.yandex-team.ru/arc/trunk/arcadia/maps/mobile/libs/search/search/idl/search/data_types.idl?rev=r7302799#L75
[endpoint]: https://a.yandex-team.ru/arc/trunk/arcadia/maps/mobile/libs/search/search/idl/search/search_manager.idl?rev=6125869#L45
[proxy]: https://a.yandex-team.ru/arc/trunk/arcadia/maps/mobile/server/proxy/config/mapkit2/locations/search.service.conf
[test_app_android]: https://a.yandex-team.ru/arc/trunk/arcadia/maps/mobile/apps/test_app/android
[android_tests]: https://a.yandex-team.ru/arc/trunk/arcadia/maps/mobile/apps/test_app/android/src/main/java/com/yandex/maps/testapp/search/test/SearchTestSuite.kt?rev=6680050#L95
[test_app_ios]: https://a.yandex-team.ru/arc/trunk/arcadia/maps/mobile/apps/test_app/ios
[ios_tests]: https://a.yandex-team.ru/arc/trunk/arcadia/maps/mobile/apps/test_app/ios/TestApp/Search/SearchTestSuite.swift
[booking]: https://st.yandex-team.ru/MAPSEARCH-3401
[modular]: https://st.yandex-team.ru/MAPSEARCH-3638
