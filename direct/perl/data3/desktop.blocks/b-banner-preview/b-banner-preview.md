r109520
Блок предпросмотра баннера.

Сюда переезжает бывший b-banner плюс элементы/блоки, которые, как мы посчитали, должны относиться к превью.

пример вызова и описание параметров:

    {
        block: 'b-banner-preview',
        banner: {
            //данные про баннер
        },
        randPhrase: u.pickRandom(group.phrases), //случайная фраза для подстановки шаблонов и параметров в ссылки
        yandexDomain: yandexDomain, //домен
        customTitle: customTitle, // передаем, если не хотим использовать заголовок из banner.title
        isTemplateBanner: isTemplateBanner, //передаем, если не хотим рассчитывать флаг isTemplateBanner по формуле !!banner.is_template_banner, а хотим задать его сами
        openInSameTab: openInSameTab, //ссылку с заголовка баннера окрываем в том же табе  (для b-banners-search-banner)
        customUrl: customUrl, //ссылка для баннера, если мы по какой-то причине не хотим использовать bannner.href (например на странице поиска по баннерам, где ссылка  с заголовка должна вести на страницу кампании)
        validateSitelinks: validateSitelinks, // нужно валидировать сайтлинки при формировании превью (для превью в b-sitelink-selector)
        hideAdditions: hideAdditions, //всегда скрывать блок "дополнения". Если не передаем -  показывается, если есть сайтлинки или картинки
        hideDomainParams: hideDomainParams, //прятать инфу про домен (для b-competitors-banners-list )
        hideVcardDetails: hideVcardDetails, //прятать инфу про визитку (для  b-competitors-banners-list )
        hideTemplateWarning: hideTemplateWarning, //прятать инфу про шаблон (для  b-competitors-banners-list)
        hideWarnings: hideWarnings, //прятать предупреждения (для b-banners-search-banner)
        showStatus: showStatus, //показывать ли блок со статусом баннера

        showGeo: showGeo, //показывать ли информацию про регион
        statusOpenStat: statusOpenStat, //подключена ли внешная интернет статистика в кампании, добавит в ссылку превью параметр _openStat
        statusClickTrack: statusClickTrack, //подключено ли отслеживание переходов в метрике, добавит в ссылку превью параметр yclid

        number: number, //номер баннера в превью группы (b-group-preview__item)
        controls: controls, //контроллы баннера в превью группы (b-group-preview__item)
        showThumbnail: showThumbnail, //показывать картинку в превью
        hideAdWarnings: hideAdWarnings, //прятать предупреждения (для превью картинки и сайтлинков)
        hideBid: {Boolean}, //не показывать номер баннера в шапке
        isEasy: {Boolean}, //отображается ли превью в легком интерфейсе
        withMobile: {Boolean}, //показывать ли в заголовке, что объявление - мобильное, если оно таковым является
        hideOngoingShowsStatus: {Boolean}, //скрывать ли статус "Идут показы предыдущей версии объявления"

        actions: actions, //хэш с доступными для баннера действиями
    }


