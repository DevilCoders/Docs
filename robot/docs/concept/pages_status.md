# Как проверить состояние страниц в базе поиска

## Вьюер Juno

[Ссылка на вьюер](https://juno.viewer.yandex-team.ru/)

Доступ к вьюеру запрашивается через [IDM](https://nda.ya.ru/t/EGt3QNnX5B8oVR)

**Вьюер Juno** — это основной вьюер базы поиска, где можно посмотреть статусы проиндексированных и посещенных страниц для поиска по HTML-страницам. По вьюеру можно посмотреть, включена ли страница в базу поиска, общее число известных страниц с домена и т.д. При этом контент страниц через вьюер посмотреть не удастся, для этого нужно использовать [вьюер KWYt](https://docs.yandex-team.ru/robot/concept/kwyt_viewer). Вьюер также не покажет данные по проиндексированным картинкам для поиска по изображениям или плееры для поиска по видео. 

[![juno_mainmenu](https://jing.yandex-team.ru/files/oddeye/browser_CBRtTvwnuv.png)](https://jing.yandex-team.ru/files/oddeye/browser_CBRtTvwnuv.png)

**1. YT Prefix** — папка, в которой расположены данные для вьюера. Данные лежат на Arnold, поэтому без специальной необходимости менять не нужно. 
**2. State** — это версия поисковой базы, для которой отображается информация о страницах. Подробнее о том, какие бывают состояния, можно прочитать в приложении ниже.
**3. Status** — Статус страницы. Данный пункт позволяет показать только страницы, с определенным статусом. К примеру, статус Indexed покажет в списке только те страницы, которые в данный момент проиндексированы роботом и находятся в базе Юпитера. Http error code покажет все страницы сайта, которые были исключены из-за какой-либо http-ошибки. Подробнее о том, какие бывают статусы, можно прочитать в примечаниях.

{% cut "Пример" %}

[![juno_states](https://jing.yandex-team.ru/files/gella/browser_WyGt8PhpA2.png)](https://jing.yandex-team.ru/files/gella/browser_WyGt8PhpA2.png)

{% endcut %}

На скриншоте можно увидеть состояние страниц в трех поисковых база: в уже прошедшей поисковой базе от 20.09.2016 (state), в текущей поисковой базе (state 1) и в следующей поисковой базе (state 2). Можно увидеть, что раньше главная страница успешно участвовала в поиске, но сейчас исключена из базы и в поиске участвует фиктивный документ страницы из-за установленного на ней перенаправления 301.}>

**4. Code** — позволяет показать только те страницы сайта, которые отвечали определенным http-кодом. К примеру, набрав 404, можно увидеть все страницы, которые отвечали на запросы робота http-кодом 404.

[![juno_404](https://jing.yandex-team.ru/files/oddeye/browser_c4OM6heBEY.png)](https://jing.yandex-team.ru/files/oddeye/browser_c4OM6heBEY.png)
Можно искать как по стандартным HTTP-кодам, так и [роботным ошибкам](https://docs.yandex-team.ru/robot/concept/robot_errors). При этом не все ошибки есть в Juno: например, ошибка 2025 (неканоническая страница) не отобразится во вьюере, вместо этого страница будет исключена как NOT MAIN URL, и в статусе страницы будет указан канонический адрес.

**5. Url** — в этом окне указывается сайт или страница, информацию по которой Вы хотите получить. Например, если ввести http://site.ru , то будет отображен весь список известных страниц. Если указать http://site.ru/catalog , то будут отображены только ссылки из раздела /catalog/. Запрос http://site.ru/catalog/some-cool-stuff.HTML отобразит информацию по странице.

{% cut "Примеры" %}

[![juno_pages1](https://jing.yandex-team.ru/files/gella/browser_wUXCqVRfwf.png)](https://jing.yandex-team.ru/files/gella/browser_wUXCqVRfwf.png)
[![juno_pages2](https://jing.yandex-team.ru/files/gella/browser_vP6jKSe6Nj.png)](https://jing.yandex-team.ru/files/gella/browser_vP6jKSe6Nj.png)
[![juno_pages3](https://jing.yandex-team.ru/files/gella/browser_afdpXDbEma.png)](https://jing.yandex-team.ru/files/gella/browser_afdpXDbEma.png)

{% endcut %}

**6. Go** — загрузить данные. Данные во вьюере не обновляются автоматически при смене каких-либо параметром, поэтому если необходимо, например, изменить набор состояний, требуется сначала указать нужные параметры state, после этого нажать на кнопку Go.

### Urlviewver

В данной вкладке можно посмотреть информацию о страницах, размещенных на домене, либо в какой-либо директории сайта. Страницы отображаются списком, в котором отображается базовая информация о статусе страницы.

{% note alert %}

Даты обращений в Juno указываются в часовом поясе саппорта, который использует базу, т.е. актуальны именно для того, кто просматривает информацию в данный момент из конкретной точки!

{% endnote %}


[![juno_urlviewer](https://jing.yandex-team.ru/files/gella/browser_ZUPDsBA6uW.png)](https://jing.yandex-team.ru/files/gella/browser_ZUPDsBA6uW.png)

**1. Адрес страницы**
**2.  Code** — код, которым отвечала страница на момент ее обхода роботом. (например, 200 ОК — страница доступна и обходится; http-403 — доступ к странице запрещен. Также могут отображаться специальные роботные коды: 2005 — страница запрещена к индексированию мета-тегом noindex. О том, какие бывают роботные коды, читать [здесь](https://docs.yandex-team.ru/robot/concept/robot_errors).
**3. Docsize** — размер документа. Размер документа обозначается не в общепринятых величинах (байты и подобное), а в условных единицах (указывается количество термов из keyinv. Значение должно коррелировать с размером в байтах).
**4. LastAccess** — дата, когда последний раз посещалась страница. Речь идет о последнем посещении в том обновлении поисковой базы, для которой выбран State.
**5. Status** — статус данной страницы в базе Юпитера.
Все данные пункты показываются отдельно для каждого State.

### Кнопки
На страницах также могут отображаться кнопки и ярлыки, которые будут указывать на определенные состояния страниц.

[![juno_buttons1](https://jing.yandex-team.ru/files/gella/browser_rHFi0KOL1M.png)](https://jing.yandex-team.ru/files/gella/browser_rHFi0KOL1M.png)

[![juno_buttons2](https://jing.yandex-team.ru/files/gella/browser_F8BZCesphd.png)](https://jing.yandex-team.ru/files/gella/browser_F8BZCesphd.png)

[![juno_buttons3](https://jing.yandex-team.ru/files/gella/browser_XrnjOruAje.png)](https://jing.yandex-team.ru/files/gella/browser_XrnjOruAje.png)

* **Redir** — страница выполняет перенаправление на другую страницу. Нажав на эту кнопку, можно открыть страницу-цель перенаправления в новом окне.
* **Mirror** — сайт является неглавным зеркалом другого сайта и данная страница отсутствует в поиске, поскольку в результатах поиска находится аналогичная страница по адресу главного зеркала. Нажав на эту кнопку, можно открыть страницу главного зеркала в новом окне.
* **To be deleted** — страница будет удалена из базы робота в следующем обновлении поисковой базы.
* **Main** — у страницы другой главный (main) URL. Нажав на кнопку, можно открыть страницу с главным URL для данной страницы.
* **Not beauty** — страница находится в поиске по другому адресу. Нажав на кнопку Beauty, можно открыть страницу, которая находится в поиске, в новой вкладке. Такая ситуация может быть, к примеру, если главная страница сайта выполняет редирект на внутреннюю страницу того же домена. Главную страницу из поиска мы не удалим, а вместо этого покажем контент внутренней, на которую идет редирект, по адресу главной.
* **Rel canonical** — для страницы указан атрибут rel="canonical". Нажав на кнопку, можно открыть указанную в качестве канонической страницу. 

### Цвета

Цвет информационного поля страницы также отображает статус страницы:
* **Зеленый** — страница проиндексирована. (Sic! Страница не обязательно находится в поиске. Страница со статусом Not beauty также может помечаться зеленым).
* **Синий** — страница проиндексирована как фиктивная. В случае, когда главная страница удаляется из поисковой базы, мы все еще можем показывать ее в поиске, находя по запросу с названием домена, либо по тексту внешних ссылок. Она будет отображаться в поиске без сохраненной копии, а в базе Юпитера будет помечаться синим цветом.
* **Красный** — страница отсутствует в поиске.

### Dupsviewer
Данный раздел позволяет посмотреть группы дублей для определенной страницы.

{% cut "Пример" %}

[![juno_dups](https://jing.yandex-team.ru/files/gella/browser_PoQOvg5MZt.png)](https://jing.yandex-team.ru/files/gella/browser_PoQOvg5MZt.png)

На скриншоте можно увидеть пример группы дублей для страницы [https://rutube.ru](https://rutube.ru) Страница индексируется по адресу [https://rutube.ru](https://rutube.ru) (main) и находится в поиске (beauty). В группу входит 94 страницы в текущей базе и 97 войдет в следующей базе.

{% endcut %}

### UrlInfo
Показывает более подробную информацию об определенной странице.

[![juno_urlinfo](https://jing.yandex-team.ru/files/oddeye/browser_D259liUarX.png)](https://jing.yandex-team.ru/files/oddeye/browser_D259liUarX.png)

1. **Url** — адрес проверяемой страницы. 
2. **Status** — статус страницы. (Indexed — проиндексирована; indexed as fake — проиндексирована как фиктивный и т.д.)
3. **Penalties** — наложенные на страницу пенальти.
4. **HttpCode** — http-код, которым страница отвечала на запросы.
5. **AddTime / LastAccess** — дата добавления страницы в базу / дата последнего посещения робота.
6. **Hops** — количество переходов до данной страницы от главной страницы сайта. Например, у главной страницы site.ru будет 0 переходов. У страницы site.ru/page1 — 1 переход. У страницы site.ru/page1/kittens — 3 перехода.
7. **IsFake** — фиктивный ли документ. Только у документов, которые в поиске находятся как фиктивные, будет стоять True, в остальных случаях — false.
8. **HasContent** — отдавала ли страница при посещении какой-либо контент. True — если отдавала, False — если нет.
9. **DocSize** — размер документа. Размер документа обозначается не в общепринятых величинах (байты и подобное), а в условных единицах (указывается количество термов из keyinv. Значение должно коррелировать с размером в байтах).
10. **BeautyUrl** — документ, который находится в поиске. Если URL в этой графе совпадает с **Url**, то страница находится в поиске по собственному адресу. Если же адрес этой страницы отличается, то в поисковой выдаче находится та страница, которая указана как Beauty. BeautyUrl может отличаться, например, из-за перенаправления 302, перенаправления с главной страницы, неглавного зеркала.
11. **IsMain** — является ли страница главной страницей в группе дублей, то есть той страницей, контент которой индексирует робот. Например, если контент страниц site.ru/dogs и site.ru/fluffy_things будет одинаковым и робот посчитает их дублями, Main будет указывать, какая из страниц главная в группе дублей.
13. **Main URL during SR** — адрес страницы, которая показывалась в поиске, если данная ссылка была удалена по SelectionRank.
14. **Main Url** — главная страница, т.е. та страница, контент которой индексируется. Будет отличаться, если **IsMain** = **false**.
15. **Main Mirror Url** — адрес страницы главного зеркала. Если сайт, url которого Вы проверяете, является главным зеркалом, то этот адрес совпадет с пунктом 1. Если же сайт является неглавным зеркалом, то здесь будет указан адрес соответствующей страницы главного зеркала.

{% cut "Пример" %}

 [![juno_afishamirror](https://jing.yandex-team.ru/files/gella/browser_XbCLyYR8ss.png)](https://jing.yandex-team.ru/files/gella/browser_XbCLyYR8ss.png)

 Сайт [http://afisha.ru](http://afisha.ru) является неглавным зеркалом [https://www.afisha.ru](https://www.afisha.ru), поэтому данная страница индексируется роботом по адресу главного зеркала [https://www.afisha.ru/movie/223558/](https://www.afisha.ru/movie/223558/).

{% endcut %}

16. **RelCanonicalTarget** — если страница содержит атрибут тега rel="canonical", здесь будет отображаться адрес канонической страницы.
17. **IsRedirect** — выполняет ли страница перенаправление на другую страницу. (True — если выполняет, False — если нет).
18. **RedirectTarget** — если страница выполняет редирект, здесь будет указана цель редиректа. (см. пример для пункта 13: страница выполняет редирект на [http://www.afisha.ru/movie/223558/](http://www.afisha.ru/movie/223558/)).
19. **Upload Ranks** — ранги для загрузки страниц в поиск по SelectionRank.
20. **Shard List with thresholds** — данные по прохождению страниц SelectionRank.

### Hostinfo

В этой вкладке находится информация по сайту в целом: количество известных на домене страниц, количество страниц в поиске и т.д.

[![juno_host](https://jing.yandex-team.ru/files/gella/browser_WeHNul4esD.png)](https://jing.yandex-team.ru/files/gella/browser_WeHNul4esD.png)

Информация во вкладке:
1. **Host** — адрес хоста, на котором расположен сайт.
2. **Status** — статус индексации данного сайта.
3. **IP** — IP-адрес данного сайта.
4. **AddTime / LastAccess** — информация о том, когда робот впервые узнал о данном сайте / когда в последний раз посетил сайт.
5. **Total urls in base** — информация о том, сколько всего страниц данного сайта нам известно.
6. **Urls indexed** — количество проиндексированных страниц.
7. **Urls indexed as fake** — количество фиктивных документов в поиске.
8. **Urls with content** — число страниц, отдающих роботу контент в ответ на запросы.
9. **Urls to be deleted form next base** — количество страниц, которые будут удалены из базы в следующем обновлении.
10. **Penalties** — количество страниц, на которые наложены различные пенальти (страницы, которые по тем или иным причинам не удалось проиндексировать или робот не стал их посещать). Подробнее о том, какие бывают пенальти, можно прочитать в примечаниях.
11. **HTTP error code** — страница отвечала http-ошибкой. Например, 404 или 500.
12. **TierStats** — статистика для SelectionRank.
13. **RobotsHTTPCode** — код ответа файла robots.txt. Если код отличается от 200, значит, файл по тем или иным причинам не удалось обработать.
14. **RobotsTxt (not exact)** — сам текст файла robots.txt на момент обновления поисковой базы. В данном разделе приводится не абсолютно точная копия файла, каким он доступен по адресу site.ru/robots.txt. Например, директивы, заданные для сторонних роботом, в этом файле не отобразятся.

### Deliveries

Содержит данные о версиях таблиц Юпитера для разработчиков.

### MultiUrlViewer
Позволяет посмотреть статусы для нескольких выбранных страниц.

{% cut "Пример" %}

[![juno_multiviewer](https://jing.yandex-team.ru/files/gella/browser_cm9I0lt9CB.png)](https://jing.yandex-team.ru/files/gella/browser_cm9I0lt9CB.png)
На скриншоте показаны состояния трех доменов в предыдущей базе (state), в текущей (state 1) и в следующей (state 2).
Каждый новый URL необходимо указывать с новой строки.

{% endcut %}

### Force Rerfresh
Обновить данные вьюера. Сбрасывает кэш во вьюере. Можно использовать, если, к примеру, возникла проблема с отображением состояний. Если не помогает, для разрешения проблемы стоит обратиться к ответственным.

# Примечания

### Статусы и пенальти

* **ErrorHttpCodePenalty** — http-код ошибки (404, 2005 и т.д.);
* **BadMimeTypePenalty** — плохой mime type;
* **HostUnavailablePenalty** — хост недоступен;
* **HostBannedByRobotTxtPenalty** — Host запрещен к индексированию в robots.txt директивой `Disallow: /`;
* **UrlBannedByRobotTxtPenalty** — url запрещен к индексированию в файле robots.txt;
* **BannedByAntispamPenalty** — url забанен Веб-антиспамом;
* **NotMainUrlPenalty** — не главный url (может появиться в случае дублирующих страниц, атрибута rel="canonical", атрибута Clean-param в robots.txt, перенаправления 301). Означает, что страница индексируется роботом по другому адресу
;

[![juno_notmainmirror](https://jing.yandex-team.ru/files/gella/browser_BvivdumvGI.png)](https://jing.yandex-team.ru/files/gella/browser_BvivdumvGI.png)

Нажав на кнопку "Main" в UrlViewer'e, можно открыть вкладку с главной (main) страницей.
* **Main200HasNoContentPenalty** — главный url не имеет контента;
* **MainNotPassedByPreSRFilterOtherReasonPenalty** — скорее всего, это редирект (если внутрихостовый — на неизвестную нам цель, если межхостовый — то не на зеркало). Если вы видите что-то другое, лучше обратиться к поддержке робота.
* **MainNotInIndexBySRPenalty** — главный url не прошел Selectionrank;
* **NoDuplicateInfoPenalty** — нет дубликатов;
* **BannedByRflPenalty** — забанен по rfl (url имеет незначащие параметры). RFL — это некий файл внутри Яндекса, схожий с robots.txt, где могут удаляться из базы get-параметры, которые дублируют контент, или, например, сайты, которые из-за ошибок в движке создают бесконечное число поддоменов;
* **RecrawledNonMainMirrorPenalty** — неглавное зеркало.

* **Виды состояний**
[![juno_da_states](https://jing.yandex-team.ru/files/gella/browser_WhMFrcSrPV.png)](https://jing.yandex-team.ru/files/gella/browser_WhMFrcSrPV.png)

* **No state** — не отображать никаких состояний. Одновременно можно отобразить от одного до трех состояний. По умолчанию при запросе отображается два: production и priemka.
* **Old** — информация о страницах в предыдущих поисковых базах.
* **Prev Production** — данные о странице в базе, которая только недавно сменила новая база.
* **Production** — состояние страницы в текущей базе.
* **Priemka** — состояние страницы в ближайшей следующей базе. 
* **New** — новая база, которая уже начала собираться, но еще не была принята. New не обязательно означает, что эта база будет принята и попадет в production, однако при успешном цикле new превратится в **priemka**.
* **?** — проблема с загрузкой базы или таблицей. При обновлении базы и создании таблиц для данных вьюера, может подхватить переключение базы раньше, чем появились таблички. Force Refresh может помочь. Если проблема сохраняется долго, стоит обратиться к ответственным.

# Данные из Яндекс.Вебмастера

Внешние пользователи получают данные об индексировании сайта из [Яндекс.Вебмастера](https://webmaster.yandex.ru/sites/). Многие из данных, которые есть в базе поиска, можно также посмотреть в Вебмастере. Если у вас новый домен, вы можете подтвердить на него права [обычным образом](https://yandex.ru/support/webmaster/service/rights.html). Для какого-либо стороннего сайта есть возможность посмотреть данные в панели администратора Вебмастера. Для этого потребуется специальный доступ, который можно получить, если есть специальная необходимость и доступы. О том, как это сделать, можно прочитать в [документации Вебмастера](https://wiki.yandex-team.ru/JandeksPoisk/Interfejjsy/CentrVebmastera/access/).

# Обратная связь
Вопросы по вьюеры и данным можно задать в чате [RobotSuppot](https://t.me/joinchat/QJXdYCa2rEOr0nLg)
