### Изначальная проблема
При выставлении у Mapper'a mapstruct'a `unmappedTargetPolicy = ReportingPolicy.ERROR`, начинает падать сборка, 
если у класса-результата маппинга есть аннотация `@With`.
### Что делает эта библиотека
Это прокси-библиотека, которая при подключении в проект автоматом подсовывает через SPI в 
`org.mapstruct.ap.spi.AccessorNamingStrategy` [класс](https://a.yandex-team.ru/arc_vcs/market/market-tpl/common/tpl-common-util/src/main/java/ru/yandex/market/tpl/common/util/mapstruct/ExcludeWithAssessorNamingStrategy.java?rev=587eb263fb919628e54b9d1bd740e58e615a9f1a#L7) 
из tpl-common-util.
### Зачем нужна отдельная библиотека
И почему нельзя просто сделать это в конкретном моделе? [Ответ](https://st.yandex-team.ru/DEVTOOLSSUPPORT-6563).