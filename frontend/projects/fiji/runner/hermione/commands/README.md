## Constants

<dl>
<dt><a href="#allowed">allowed</a></dt>
<dd><p>Разрешенные поля из объекта в формате ShareData <a href="https://w3c.github.io/web-share/#sharedata-dictionary">https://w3c.github.io/web-share/#sharedata-dictionary</a>
Проверка заточена под шаринг двух видов:</p>
<ul>
<li>одна ссылка</li>
<li>ссылка и текстовая аннотация
Умышленно не разрешаем <code>text</code> (хотя он есть в спеке ShareData) – следует использовать <code>title</code> для любого текста.
Причины и примеры:
1) Если разложить в <code>title</code> и <code>text</code>, то чаще всего приложения используют только <code>text</code>
 (и не используют <code>title</code>), что странно, т.к. заголовок как правило важнее.
 К примеру на Android после &#39;Copy to clipboard&#39; из попапа в буфере обмена окажется
 строчка &#39;{text} {url}&#39; - без заголовка.
2) В iOS есть фича, которая при шаринге подтягивает со страницы мета-информацию и в шапке попапа рисует
 картинку с заголовком. Фича крутая и важно её не потерять, и она перестает работать, если задан <code>text</code>.</li>
</ul>
<p>2.1) Если передать <code>title</code> + <code>text</code> + <code>url</code>, то в шапке попапа будет виден <code>text</code>,
     в случае организации это ее адрес, скрин: <a href="https://nda.ya.ru/t/yMYUawME3W286c">https://nda.ya.ru/t/yMYUawME3W286c</a>.
     После &#39;Copy&#39; из попапа в буфере обмена окажется строчка &#39;{text} {url}&#39; - без заголовка.
2.2) А если передать <code>title</code> + <code>url</code>, то сначала в шапке отобразится хост (yandex.ru),
     скрин: <a href="https://nda.ya.ru/t/JPl795z63W287D">https://nda.ya.ru/t/JPl795z63W287D</a>, а спустя пару секунд подгрузится мета-информаниция
     и появится заголовок и картинка, скрин: <a href="https://nda.ya.ru/t/tOhAzMUZ3W287H">https://nda.ya.ru/t/tOhAzMUZ3W287H</a>.
     <code>title</code> при этом судя по всему не используется.</p>
</dd>
</dl>

## Functions

<dl>
<dt><a href="#addDirectWidgetScript">addDirectWidgetScript()</a> ⇒ <code>*</code></dt>
<dd><p>Добавляем скрипт виджета директа</p>
</dd>
<dt><a href="#assertViewCropViewport">assertViewCropViewport()</a></dt>
<dd><p>Делает скриншот элемента, но только в пределе вьюпорта</p>
</dd>
<dt><a href="#clearCounters">clearCounters()</a> ⇒ <code>*</code></dt>
<dd><p>Очищаем объект со счётчиками</p>
</dd>
<dt><a href="#clickTo">clickTo(selector, clientX, clientY)</a> ⇒ <code>Promise</code></dt>
<dd><p>Клик в определенную точку элемента</p>
</dd>
<dt><a href="#closeOtherTabs">closeOtherTabs()</a> ⇒ <code>Promise</code></dt>
<dd><p>Закрывает все открытые в браузере вкладки кроме первой</p>
</dd>
<dt><a href="#disableAnimation">disableAnimation()</a></dt>
<dd><p>Отключает анимацию на всех блоках</p>
</dd>
<dt><a href="#disableStickyPlayer">disableStickyPlayer(stickyContentSelector)</a> ⇒ <code>*</code></dt>
<dd><p>Отлепляем плеер</p>
</dd>
<dt><a href="#enableExternalLinks">enableExternalLinks(linksMode)</a></dt>
<dd><p>Управляет внешними ссылками на странице
Подробности тут: .templar/testing/assets/assets-hermione/common/no-external-links.js</p>
</dd>
<dt><a href="#enableInternalLinks">enableInternalLinks(linksMode)</a></dt>
<dd><p>Управляет относительными ссылками на странице
Подробности тут: .templar/testing/assets/assets-hermione/common/no-external-links.js</p>
</dd>
<dt><a href="#fakeTimerTick">fakeTimerTick(timeout, restore)</a></dt>
<dd><p>Делает тик фейкового таймера</p>
</dd>
<dt><a href="#focus">focus()</a> ⇒ <code>*</code></dt>
<dd><p>Чинит баг в firefox про неправильную работу keys
Подробности:
<a href="https://gitter.im/webdriverio/webdriverio?at=55f04dda5ba1e0ea6b804aca">https://gitter.im/webdriverio/webdriverio?at=55f04dda5ba1e0ea6b804aca</a>
<a href="https://gitter.im/webdriverio/webdriverio?at=55f0b62f24362d5253fe7c37">https://gitter.im/webdriverio/webdriverio?at=55f0b62f24362d5253fe7c37</a></p>
</dd>
<dt><a href="#getCounter">getCounter(counter, [timeout], [reverse])</a> ⇒ <code>Promise</code></dt>
<dd><p>Возвращает параметры отправленного счётчика
Пробует каждые 100 ms получить этот счётчик в течение {timeout} или 1 секунды</p>
<p>Если вам нужно проверить, что счётчик не отправляется — используйте параметр reverse!</p>
</dd>
<dt><a href="#getCounterByDecoded">getCounterByDecoded(decoded, [timeout], [reverse])</a> ⇒ <code>Promise</code></dt>
<dd><p>Ждет, пока в mm.counters появится счетчик с указанным decoded или совпадающий по regexp
Пробует каждые 200 получить этот счётчик в течение {timeout} или 1 секунды</p>
</dd>
<dt><a href="#getCounterByName">getCounterByName(name, [timeout], [reverse])</a> ⇒ <code>Promise</code></dt>
<dd><p>Ждет, пока в mm.counters появится счетчик с указанным name
Пробует каждые 200 получить этот счётчик в течение {timeout} или 1 секунды</p>
</dd>
<dt><a href="#getCounterByPath">getCounterByPath(path, [timeout], [reverse])</a> ⇒ <code>Promise</code></dt>
<dd><p>Ждет, пока в mm.counters появится счетчик с указанным path
Пробует каждые 200 получить этот счётчик в течение {timeout} или 1 секунды</p>
</dd>
<dt><a href="#getPlayerFrame">getPlayerFrame()</a> ⇒ <code>Promise</code></dt>
<dd><p>Возвращает html плеера</p>
</dd>
<dt><a href="#getPlayerFrameSrc">getPlayerFrameSrc()</a></dt>
<dd><p>Возвращает html плеера</p>
</dd>
<dt><a href="#getPlayerId">getPlayerId()</a></dt>
<dd><p>Возвращает playerId</p>
</dd>
<dt><a href="#getPlayerTestAttr">getPlayerTestAttr()</a></dt>
<dd><p>Возвращает html плеера</p>
</dd>
<dt><a href="#getReduxStateValue">getReduxStateValue(path)</a> ⇒ <code>*</code></dt>
<dd><p>Достает из стейта Redux-стора значение по строковому пути, переданному в функцию
Бросает ошибку, если стора нет в глобальной переменной <strong>reduxStore</strong>
или если по указанному пути не найдено значение</p>
</dd>
<dt><a href="#getReqId">getReqId(element, [attr])</a> ⇒ <code>Promise</code></dt>
<dd><p>Вытаскиваем ReqId из указанного элемента.</p>
</dd>
<dt><a href="#getScrollPosition">getScrollPosition(element)</a> ⇒ <code>Promise</code></dt>
<dd><p>Получаем позицию скрола у скролируемой области</p>
</dd>
<dt><a href="#getVideoData">getVideoData(element)</a> ⇒ <code>Promise</code></dt>
<dd><p>Возвращает данные ролика из указанного элемента</p>
</dd>
<dt><a href="#getViewerReqid">getViewerReqid([reduxStatePath])</a> ⇒ <code>Promise</code></dt>
<dd><p>Вытаскиваем reqid из состояния redux-хранилища,
если передан путь до объекта в сторе, содержащего поле reqid
Берем из начальных пропсов, если путь не передан</p>
</dd>
<dt><a href="#openSPASFromWeb4">openSPASFromWeb4(urlOptions)</a> ⇒ <code>Webdriverio</code></dt>
<dd><p>Перед переходом на страницу сценария сначала открывает СЕРП с флагами SPAS.
После открытия СЕРПа происходит SPAS переход на адрес сценария.</p>
</dd>
<dt><a href="#goSPASURL">goSPASURL(opts)</a> ⇒ <code>Webdriverio</code></dt>
<dd><p>Имитирует открытие урла с помощью библиотеки search-spa.
Переход на переданный URL произойдёт с помощью AJAX-перехода со страницы web4.</p>
</dd>
<dt><a href="#goURL">goURL(opts)</a> ⇒ <code>Webdriverio</code></dt>
<dd><p>Переход по URL</p>
</dd>
<dt><a href="#loadNextVideoPage">loadNextVideoPage(currentPage)</a> ⇒ <code>*</code></dt>
<dd><p>Загружает новую страницу сниппетов для всех страниц Видео
(Морда, Поиск, Мои Видео)</p>
</dd>
<dt><a href="#makeTransparent">makeTransparent(selector, mode)</a></dt>
<dd><p>Делает элементы по селектору прозрачными</p>
</dd>
<dt><a href="#preparePageForScroll">preparePageForScroll()</a> ⇒ <code>*</code></dt>
<dd><p>Подготовка страницы к скроллу (скрытие шапки, включение скоролла)</p>
</dd>
<dt><a href="#reStubImage">reStubImage()</a> ⇒ <code>Promise.&lt;Boolean&gt;</code></dt>
<dd><p>Меняет параметры mmui-png-stub</p>
</dd>
<dt><a href="#retryActionsByElemNotVisible">retryActionsByElemNotVisible(retries, selector, action)</a> ⇒ <code>Promise</code></dt>
<dd><p>Метод, который позволяет циклично выполнять последовательные действия в браузере
пока не пропадёт заданный элемент. Действия необязательно должны производиться над элементом</p>
</dd>
<dt><a href="#retryActionsByElemVisible">retryActionsByElemVisible(retries, selector, action)</a> ⇒ <code>Promise</code></dt>
<dd><p>Метод, который позволяет циклично выполнять последовательные действия в браузере
пока не появится искомый элемент. Действия необязательно должны производиться над элементом</p>
</dd>
<dt><a href="#saveReqId">saveReqId(stateObject, element, [attr])</a> ⇒ <code>Promise</code></dt>
<dd><p>Сохраняем текущий ReqID элемента чтобы потом проверить что он изменился в waitForReqId</p>
</dd>
<dt><a href="#scrollIntoView">scrollIntoView(element, [params])</a> ⇒ <code>Promise</code></dt>
<dd><p>Насильно скроллим к элементу при помощи JS в браузере.</p>
</dd>
<dt><a href="#sendPlayerEvent">sendPlayerEvent(event, [data])</a></dt>
<dd><p>Инициирует отправку события плеера</p>
</dd>
<dt><a href="#setPlayerTestAttr">setPlayerTestAttr()</a></dt>
<dd><p>Возвращает html плеера</p>
</dd>
<dt><a href="#setReactInputValue">setReactInputValue()</a> ⇒ <code>Promise</code></dt>
<dd><p>Имитирует очистку инпута нажатиями кнопки BACKSPACE, а затем записывает строку в инпут
Обычный setValue не подойдет, т.к. встроенная в этот метод очистка не работает
React слушает событие изменения значения инпута, которое не триггерится при очистке</p>
</dd>
<dt><a href="#tickPlayerTimer">tickPlayerTimer(timeout)</a></dt>
<dd><p>Делает тик таймера в песочнице</p>
</dd>
<dt><a href="#waitForImagesLoaded">waitForImagesLoaded(selector)</a> ⇒ <code>Promise</code></dt>
<dd><p>Ожидает пока загрузятся картинки, удовлетворяющие заданному селектору</p>
</dd>
<dt><a href="#waitForItemLoaded">waitForItemLoaded(selector)</a> ⇒ <code>Promise</code></dt>
<dd><p>Ожидает пока загрузится/перезагрузится указанный элемент выдачи</p>
<p>Ожидает элемент выдачи, у которого не стоит атрибут loaded=yes, после загрузки устанавливает его
Соответственно, если к элементу уже был вызов функции, то последующий вызов не зарезолвится
до тех пор, пока страница не будет перезагружена или выдача не перестроиться</p>
</dd>
<dt><a href="#waitForAbsent">waitForAbsent(selectors, options)</a> ⇒ <code>Promise</code></dt>
<dd><p>Функция позволяет дождаться,
пока элемент пропадёт,
если он в текущий момент присутствует на странице.</p>
</dd>
<dt><a href="#waitForLoad">waitForLoad()</a> ⇒ <code>*</code></dt>
<dd><p>Ожидаем когда пропадет fade и появится .b-page_js_inited для выдачи и #root.root_inited для просмотрщика</p>
</dd>
<dt><a href="#waitForNewTab">waitForNewTab([timeout], [reverse])</a> ⇒ <code>Promise</code></dt>
<dd><p>Ожидаем когда будет открыта новая вкладка(ки)
Проверяем на количество активных вкладок каждые 200 мс в течении {timeout} или 3 секунд</p>
</dd>
<dt><a href="#waitForPlayerLoaded">waitForPlayerLoaded([timeout])</a> ⇒ <code>Promise</code></dt>
<dd><p>Ожидает загрузки стаба плеера</p>
</dd>
<dt><a href="#waitForReqIdToChange">waitForReqIdToChange(stateObject, element, [options])</a> ⇒ <code>Promise</code></dt>
<dd><p>Проверяем текущий ReqID элемента сравнивая его с сохраненным в saveReqId</p>
</dd>
<dt><a href="#waitForSrcToChange">waitForSrcToChange(stateObject, element, [options], [timeoutMsg])</a> ⇒ <code>Promise</code></dt>
<dd><p>Проверяем текущий src элемента сравнивая его с сохраненным ранее (в saveSrc?)</p>
</dd>
<dt><a href="#waitForUrl">waitForUrl(predicate, msg)</a> ⇒ <code>Promise</code></dt>
<dd><p>Ожидание условия в текущем URL.
Есть баг в webdriver. Если не указать msg, ничего не будет работать.</p>
</dd>
<dt><a href="#yaApiClearCallHistory">yaApiClearCallHistory()</a> ⇒ <code>Promise</code></dt>
<dd><p>Очищает историю вызовов методов YandexAppsAPI</p>
</dd>
<dt><a href="#yaCheckApiOpenRelatedQuery">yaCheckApiOpenRelatedQuery(params, [timeout])</a> ⇒ <code>Promise</code></dt>
<dd><p>Проверка работы метода API openRelatedQuery</p>
</dd>
<dt><a href="#yaCheckCanonical">yaCheckCanonical()</a> ⇒ <code>Promise</code></dt>
<dd><p>Проверка canonical-ссылки. Возвращает текущий url и каноническую ссылку</p>
</dd>
<dt><a href="#yaCheckClientCounter">yaCheckClientCounter()</a> ⇒ <code>Promise</code></dt>
<dd><p>Проверяет срабатывание клиентских счетчиков (они же счетчики действий, они же редир-счетчики) по редир-логу
Если рекид не задан, то выполняется фоллбек на глобальный рекид страницы
Это сработает, например, если проверяется счетчик для картинки с первой страницы выдачи</p>
<ul>
<li>@param {String} reqid - рекид счетчика</li>
<li>@param {CounterObject|CounterObject[]} expected - Клиентские счётчики (счётчик), которые должны сработать</li>
<li>@param {String} [message] - Сообщение, если счётчик не сработал</li>
<li>@param {CounterOptions} [options]</li>
</ul>
<p>options.shouldNotBeTriggered - проверяет, что счетчик не был вызван.</p>
</dd>
<dt><a href="#yaCheckDeeplink">yaCheckDeeplink(selector, [message], noFallback)</a> ⇒ <code>Promise</code></dt>
<dd></dd>
<dt><a href="#yaCheckLinkOpener">yaCheckLinkOpener(selector, [message], [params])</a> ⇒ <code>Promise.&lt;Url&gt;</code></dt>
<dd><p>Команда для базовых проверок ссылки</p>
<ol>
<li>Атрибут href ссылки не пуст и не состоит из пробельных символов</li>
<li>Ссылка открывается с правильным атрибутом &#39;target&#39;</li>
<li>По ссылке можно кликнуть</li>
</ol>
</dd>
<dt><a href="#yaCheckPassportUrl">yaCheckPassportUrl()</a> ⇒ <code>Promise</code></dt>
<dd><p>Проверка ссылки перехода на паспорт</p>
</dd>
<dt><a href="#yaCheckServerCounter">yaCheckServerCounter()</a> ⇒ <code>Promise</code></dt>
<dd><p>Проверяет срабатывание серверных счетчиков (они же блокстат-счетчики, они же счетчики показа) по блокстат-логу</p>
<ul>
<li>@param {String} reqid</li>
<li>@param {CounterObject|CounterObject[]} expected - Серверные счётчики (счётчик), которые должны сработать</li>
<li>@param {String} [message] - Сообщение, если счётчик не сработал</li>
<li>@param {CounterOptions} [options]</li>
</ul>
</dd>
<dt><a href="#yaCheckText">yaCheckText()</a> ⇒ <code>Promise</code></dt>
<dd><p>Проверка текста, содержащегося в элементе</p>
</dd>
<dt><a href="#yaCheckURL">yaCheckURL(actualUrl, expectedUrl, [message], [params])</a></dt>
<dd><p>Команда для проверки URL</p>
</dd>
<dt><a href="#yaChooseCbirFile">yaChooseCbirFile(filePath)</a> ⇒ <code>Promise</code></dt>
<dd><p>Загружает файл в поиск по картинке (Сибирь) через кнопку фотоаппарата в стрелке</p>
</dd>
<dt><a href="#yaCleanSessionStorage">yaCleanSessionStorage(storageKey)</a> ⇒ <code>Promise</code></dt>
<dd><p>Команда для очистки sessionStorage</p>
</dd>
<dt><a href="#yaClearImagesFilter">yaClearImagesFilter()</a></dt>
<dd><p>Сбрасывает активные фильтры сервиса Картинки</p>
</dd>
<dt><a href="#yaCloseDirect">yaCloseDirect(selector)</a></dt>
<dd><p>Эмуляция закрытия блока директа</p>
</dd>
<dt><a href="#yaCloseMiniSuggest">yaCloseMiniSuggest()</a></dt>
<dd><p>Закрывает саджест (mini-suggest)
В некоторых сценариях оверлей mini-suggest__overlay ломает тесты, если его не закрыть
Возвращает промис по закрытию оверлея</p>
</dd>
<dt><a href="#yaCloseSafariTabs">yaCloseSafariTabs()</a> ⇒ <code>Promise</code></dt>
<dd><p>Закрывает лишние открытые табы при выполнении теста в мобильном safari.
TODO: использовать плагин hermione-tabs-closer после - <a href="https://st.yandex-team.ru/FEI-24830">https://st.yandex-team.ru/FEI-24830</a></p>
</dd>
<dt><a href="#yaExecuteInFrame">yaExecuteInFrame(actions, iframeSelector)</a></dt>
<dd><p>переключает на контекст iframe коллекций и
выполняет указанные действия</p>
</dd>
<dt><a href="#normalizeExpectationsResults">normalizeExpectationsResults()</a></dt>
<dd><p>Нормализует результаты &quot;expectation&quot;-ов</p>
</dd>
<dt><a href="#yaExpectOnPage">yaExpectOnPage(config, [timeout])</a> ⇒ <code>Promise</code></dt>
<dd><p>Выполняет проверки сразу после загрузки страницы</p>
</dd>
<dt><a href="#yaExtendArea">yaExtendArea()</a> ⇒ <code>*</code></dt>
<dd><p>Расширяем зону снимка вокруг выбранного блока</p>
</dd>
<dt><a href="#yaForceRelativePosition">yaForceRelativePosition(selector)</a> ⇒ <code>Promise.&lt;DOMRect&gt;</code></dt>
<dd><p>Проставляет элементу position: relative.
Данную команду надо применять для элементов с position: fixed или sticky,
чтобы на скриншотах не было дублирование.</p>
</dd>
<dt><a href="#yaGetAttributes">yaGetAttributes(selector, attributeName)</a> ⇒ <code>Promise.&lt;Array.&lt;String&gt;&gt;</code></dt>
<dd><p>Получить значения атрибута для DOM-элементов.</p>
<p>Отличия от существующего getAttribute(selector, attributeName):</p>
<ul>
<li>не генерирует ошибку, если не находит ни одного элемента по селектору</li>
<li>всегда возвращает массив (getAttribute возвращает строку, если находит только один элемент)</li>
</ul>
</dd>
<dt><a href="#yaGetBoundingClientRect">yaGetBoundingClientRect(selector)</a> ⇒ <code>Promise.&lt;DOMRect&gt;</code></dt>
<dd><p>Получает геометрию элемента на странице</p>
</dd>
<dt><a href="#yaGetCbirCropRect">yaGetCbirCropRect()</a></dt>
<dd><p>Получает геометрию элемента на странице</p>
</dd>
<dt><a href="#yaGetComputedStyle">yaGetComputedStyle(selector)</a> ⇒ <code>Promise.&lt;CSSStyleDeclaration&gt;</code></dt>
<dd><p>Получает все значения CSS свойств элементов после применения стилей</p>
</dd>
<dt><a href="#yaGetDirectId">yaGetDirectId(selector)</a></dt>
<dd><p>Получение площадки блока директа</p>
</dd>
<dt><a href="#yaGetElementIndex">yaGetElementIndex(selector)</a> ⇒ <code>Number</code></dt>
<dd><p>Возвращает индекс элемента в списке соседних нод для своей родительской ноды</p>
</dd>
<dt><a href="#yaGetGlobalParam">yaGetGlobalParam(key)</a> ⇒ <code>Promise</code></dt>
<dd><p>Возвращает значение параметра в блоке i-global</p>
</dd>
<dt><a href="#yaGetInlineStyle">yaGetInlineStyle(selector)</a> ⇒ <code>Promise.&lt;CSSStyleDeclaration&gt;</code></dt>
<dd><p>Получает все значения инлайновых CSS свойств элемента</p>
</dd>
<dt><a href="#yaGetTexts">yaGetTexts(selector)</a> ⇒ <code>Promise.&lt;Array.&lt;String&gt;&gt;</code></dt>
<dd><p>Получить текст всех найденных DOM-элементов.</p>
<p>Отличия от существующего getText(selector):</p>
<ul>
<li>ищет текст у всех найденных DOM-элементов, а не только для первого</li>
<li>возвращает текст даже для скрытых элементов</li>
</ul>
</dd>
<dt><a href="#yaHideDeviceKeyboard">yaHideDeviceKeyboard()</a></dt>
<dd><p>Прячет клавиатуру только для тех браузеров, которые это умеют</p>
</dd>
<dt><a href="#yaHideElements">yaHideElements(selectors, [mode])</a> ⇒ <code>Promise</code></dt>
<dd><p>Скрывает элементы по селекторам</p>
</dd>
<dt><a href="#yaInjectStyle">yaInjectStyle()</a></dt>
<dd><p>Объявляет переданный стиль для переданного селектора</p>
</dd>
<dt><a href="#yaKeyPress">yaKeyPress(codes)</a> ⇒ <code>Promise</code></dt>
<dd><p>Управление клавиатурой</p>
</dd>
<dt><a href="#yaMiniSuggestClick">yaMiniSuggestClick(selector, [retry])</a> ⇒ <code>Promise</code></dt>
<dd><p>Клик в элемент mini-suggest на тачах после появления саджеста.
В mini-suggest&#39;е на тачах при открытии саджеста происходит фриз кликов на 500мс,
из-за этого тесты моргают тесты моргают
<a href="https://a.yandex-team.ru/arc_vcs/frontend/packages/mini-suggest/touch.blocks/mini-suggest/mini-suggest.js?rev=be27f8e3585169a94f28f418c6f95a5d8e953b54#L21">https://a.yandex-team.ru/arc_vcs/frontend/packages/mini-suggest/touch.blocks/mini-suggest/mini-suggest.js?rev=be27f8e3585169a94f28f418c6f95a5d8e953b54#L21</a></p>
</dd>
<dt><a href="#yaMockXHR">yaMockXHR(options)</a></dt>
<dd><p>jsdoc для удобства взят из файла .config/templar/testing/assets/assets-hermione/common/mockXHR.js</p>
<p>Функция для организации стабов/моков аяксовых запросов.
Реализована с помощью подмены оригинального метода open из XMLHttpRequest
Перехватывает запросы по подходящим урлам (задаются в опциях) и отдаёт необходимые данные без сетевого запроса
Все остальные запросы осуществляются как обычно</p>
</dd>
<dt><a href="#yaMoveAndClick">yaMoveAndClick(selector, x, y)</a> ⇒ <code>Promise</code></dt>
<dd><p>Клик в элемент по координатам.
(т.к. leftClick не работает в FF)</p>
</dd>
<dt><a href="#yaOpenImageViewer">yaOpenImageViewer(options)</a></dt>
<dd><p>Функция для открытия просмотрщика картинок</p>
</dd>
<dt><a href="#yaOpenImagesFilter">yaOpenImagesFilter()</a></dt>
<dd><p>Отображает список фильтров сервиса Картинки, если он скрыт</p>
</dd>
<dt><a href="#yaOpenPageAndWaitSelector">yaOpenPageAndWaitSelector(options)</a> ⇒ <code>Promise</code></dt>
<dd><p>Открывает заданную страницу с параметрами и дожидается отображения элемента на странице</p>
</dd>
<dt><a href="#yaParseUrl">yaParseUrl()</a> ⇒ <code>Promise.&lt;Url&gt;</code></dt>
<dd><p>Получить и распарсить текущий URL</p>
</dd>
<dt><a href="#yaPassportLogin">yaPassportLogin(PO, login, password)</a> ⇒ <code>Promise</code></dt>
<dd><p>Хелпер для быстрой авторизации в паспорте</p>
</dd>
<dt><a href="#yaPatchResponse">yaPatchResponse(params)</a></dt>
<dd><p>Патч для ответов XmlHttpRequest.</p>
<p>Если нужно успеть перехватить запросы при загрузке страницы,
то нужно добавить в desiredCapabilities поле pageLoadStrategy=&#39;none&#39;.
Тогда goURL не будет ждать события load.</p>
</dd>
<dt><a href="#yaPauseAjaxStubs">yaPauseAjaxStubs(paused)</a></dt>
<dd><p>Приостанавливает или возобновляет все ajax стабы</p>
</dd>
<dt><a href="#yaRemoveLocalStorageItem">yaRemoveLocalStorageItem(keyName)</a></dt>
<dd><p>Удаляет запись из localStorage по имени ключа</p>
</dd>
<dt><a href="#yaScroll">yaScroll(selector, alignToTop)</a></dt>
<dd><p>Скролит вьюпорт к нужному элементу</p>
</dd>
<dt><a href="#yaScrollContainerToElem">yaScrollContainerToElem(elem, container)</a> ⇒ <code>Promise</code></dt>
<dd><p>Скролит родителя к указанному дочернему элементу</p>
</dd>
<dt><a href="#yaScrollElement">yaScrollElement(selector, top, left)</a></dt>
<dd><p>Скролит элемент на указанное количество пикселей</p>
</dd>
<dt><a href="#yaScrollPage">yaScrollPage(value)</a></dt>
<dd><p>Скролит страницу на указанное количесвто пикселей с учетом особенностей браузеров грида</p>
</dd>
<dt><a href="#yaScrollPageToBottom">yaScrollPageToBottom()</a></dt>
<dd><p>Скролит страницу, пока не достигнет её конца.
Это нужно для тех случаев, когда на странице есть блоки, которые по скроллу добавляют на страницу контент.</p>
</dd>
<dt><a href="#yaSetGlobalParam">yaSetGlobalParam(key, value)</a> ⇒ <code>Promise</code></dt>
<dd><p>Устанавливает значение параметра в блоке i-global</p>
</dd>
<dt><a href="#yaSetLocalStorageItem">yaSetLocalStorageItem(key, value)</a></dt>
<dd><p>Добаляет запись в localStorage</p>
</dd>
<dt><a href="#yaShouldBeSame">yaShouldBeSame(s1, s2, [message])</a> ⇒ <code>Boolean</code></dt>
<dd><p>Проверяет что два селектора указывает на один и тот же узел</p>
</dd>
<dt><a href="#yaShouldBeSizeable">yaShouldBeSizeable(selector, [message])</a> ⇒ <code>Promise.&lt;Boolean&gt;</code></dt>
<dd><p>Проверяет что элемент имеет ненулевой размер</p>
</dd>
<dt><a href="#yaShouldBeVisible">yaShouldBeVisible(selector, [message])</a> ⇒ <code>Promise.&lt;Boolean&gt;</code></dt>
<dd><p>Проверяет, что элемент видим в данный момент. Если показа не нужно ждать, лучше использовать yaShouldBeVisible,
а не waitForVisible. Если по селектору выберется несколько элементов, выбросит ошибку.</p>
</dd>
<dt><a href="#yaShouldBeVisibleWithinViewport">yaShouldBeVisibleWithinViewport(selector, [message])</a> ⇒ <code>Promise.&lt;Boolean&gt;</code></dt>
<dd><p>Проверяет, что элемент видим и находится в пределах вьюпорта.
Если по селектору выберется несколько элементов, выбросит ошибку.</p>
</dd>
<dt><a href="#yaShouldExist">yaShouldExist(selector, [message])</a> ⇒ <code>Promise.&lt;Boolean&gt;</code></dt>
<dd><p>Проверяет, что элемент существует на странице в данный момент.
Если появления ноды в DOM не нужно ждать, лучше использовать yaShouldExist, а не waitForExist</p>
</dd>
<dt><a href="#yaShouldNotBeVisible">yaShouldNotBeVisible(selector, message)</a> ⇒ <code>Promise.&lt;Boolean&gt;</code></dt>
<dd><p>Проверяет, что элемент невидим/отсутствует в данный момент.
Если скрытия не нужно ждать, лучше использовать yaShouldNotBeVisible, а не yaWaitForHidden.
Если по селектору выберется несколько элементов, выбросит ошибку.</p>
</dd>
<dt><a href="#yaShouldNotExist">yaShouldNotExist(selector, [message])</a> ⇒ <code>Promise.&lt;Boolean&gt;</code></dt>
<dd><p>Проверяет, что элемент отсутствует на странице в данный момент.</p>
</dd>
<dt><a href="#yaShowAquar">yaShowAquar()</a> ⇒ <code>Promise.&lt;Boolean&gt;</code></dt>
<dd><p>Выводит ссылки на сессии из Аквар (<a href="https://nerevar.at.yandex-team.ru/611">https://nerevar.at.yandex-team.ru/611</a>), не все сессии лежат в одной табличке,
поэтому тут несколько ссылок, в них есть метрики и все счётчики которые были вызваны на сервере и клиенте</p>
</dd>
<dt><a href="#yaSimulatedMouseDrag">yaSimulatedMouseDrag(selector, onX, onY)</a> ⇒ <code>Promise</code></dt>
<dd><p>Выполняет перетаскивание элемента мышью на заданное значение X и Y.
Последовательно генерирует 3 события: mousedown, mousemove, mouseup.
Начальной точкой перетаскивания является центр DOMRect элемента.</p>
</dd>
<dt><a href="#yaSimulatedSwipe">yaSimulatedSwipe(selector, onX, onY, inAnimationFrame)</a> ⇒ <code>Promise</code></dt>
<dd><p>Выполняет свайп на заданное значение X и Y.
Последовательно генерирует 3 события: touchstart, touchmove, touchend.
Начальной точкой свайпа является центр DOMRect элемента.</p>
</dd>
<dt><a href="#yaStubBeforeUnloadEvents">yaStubBeforeUnloadEvents(enabled)</a></dt>
<dd><p>Устанавливает или снимает stub на BeforeUnloadEvent события.
Для установки стаба нужно передать true в enables, для снятия - false.</p>
</dd>
<dt><a href="#yaToggleCssTransitions">yaToggleCssTransitions(enabled)</a> ⇒ <code>*</code></dt>
<dd><p>Включает анимации, отключённые в гермионе по умолчанию</p>
</dd>
<dt><a href="#yaTouch">yaTouch(selector, forceClickPlatforms)</a> ⇒ <code>Promise</code></dt>
<dd><p>Тач клик на элемент</p>
</dd>
<dt><a href="#yaUnpinHeader">yaUnpinHeader()</a></dt>
<dd><p>Отключает залипание шапки для тестов</p>
</dd>
<dt><a href="#yaUnstubViewerCbirUrl">yaUnstubViewerCbirUrl()</a> ⇒ <code>Promise.&lt;Boolean&gt;</code></dt>
<dd><p>Убирает ссылку на заглушку с кнопки поиска по картинке</p>
</dd>
<dt><a href="#yaWaitForAttributeChange">yaWaitForAttributeChange(selector, attr, prevValue)</a> ⇒ <code>Promise.&lt;string&gt;</code></dt>
<dd><p>Ожидает пока поменяется атрибут у элемента.</p>
</dd>
<dt><a href="#yaWaitForCbirId">yaWaitForCbirId()</a> ⇒ <code>Promise.&lt;Boolean&gt;</code></dt>
<dd><p>Ждёт появления cbir_id в урле страницы</p>
</dd>
<dt><a href="#yaWaitForCbirOriginalImageUrl">yaWaitForCbirOriginalImageUrl()</a> ⇒ <code>Promise.&lt;Boolean&gt;</code></dt>
<dd><p>Ждёт появления url в урле страницы</p>
</dd>
<dt><a href="#yaWaitForComputedStyle">yaWaitForComputedStyle(selector, source, [message])</a> ⇒ <code>Promise</code></dt>
<dd><p>Ждёт изменение CSS свойств элемента</p>
</dd>
<dt><a href="#yaWaitForHidden">yaWaitForHidden(selector, [timeout], [message])</a> ⇒ <code>Promise</code></dt>
<dd><p>Обёртка над стандартной командой waitForVisible. Позволяет указывать произвольное сообщение об ошибке.
Чтобы дождаться скрытия элемента webdriver.io предлагает использовать waitForVisible(selector, timeout, true),
что выглядит непонятно.</p>
</dd>
<dt><a href="#yaWaitForInlineStyle">yaWaitForInlineStyle(selector, source, [message])</a> ⇒ <code>Promise</code></dt>
<dd><p>Ждёт изменение инлайновых CSS свойств элемента</p>
</dd>
<dt><a href="#yaWaitForUrlChange">yaWaitForUrlChange(prevUrl)</a> ⇒ <code>Promise.&lt;Boolean&gt;</code></dt>
<dd><p>Ждёт измнение урла страницы</p>
</dd>
<dt><a href="#yaWaitForVisible">yaWaitForVisible(selector, [timeout | message], [message])</a> ⇒ <code>Promise</code></dt>
<dd><p>Обёртка над стандартной командой waitForVisible. Позволяет указывать произвольное сообщение об ошибке.</p>
</dd>
<dt><a href="#yaWaitImageLoaded">yaWaitImageLoaded(selector, [timeout], [message])</a> ⇒ <code>Promise</code></dt>
<dd><p>Проверяет, что картинка/фоновое изображение(любого блока) загрузилась.</p>
</dd>
</dl>

## Typedefs

<dl>
<dt><a href="#Position">Position</a> : <code>&#x27;left-top&#x27;</code> | <code>&#x27;right-top&#x27;</code> | <code>&#x27;center-top&#x27;</code> | <code>&#x27;left-bottom&#x27;</code> | <code>&#x27;right-bottom&#x27;</code> | <code>&#x27;center-bottom&#x27;</code> | <code>&#x27;center-center&#x27;</code> | <code>&#x27;left-center&#x27;</code> | <code>&#x27;right-center&#x27;</code></dt>
<dd><p>Функция клика по области элемента. Нужно для проверки того, что элемент кликабелен
не только в какой-то определенной области, а весь целиком</p>
</dd>
<dt><a href="#yaWaitUntilMessageCallback">yaWaitUntilMessageCallback</a> ⇒ <code>string</code></dt>
<dd></dd>
</dl>

<a name="allowed"></a>

## allowed
Разрешенные поля из объекта в формате ShareData https://w3c.github.io/web-share/#sharedata-dictionary
Проверка заточена под шаринг двух видов:
- одна ссылка
- ссылка и текстовая аннотация
Умышленно не разрешаем `text` (хотя он есть в спеке ShareData) – следует использовать `title` для любого текста.
Причины и примеры:
1) Если разложить в `title` и `text`, то чаще всего приложения используют только `text`
   (и не используют `title`), что странно, т.к. заголовок как правило важнее.
   К примеру на Android после 'Copy to clipboard' из попапа в буфере обмена окажется
   строчка '{text} {url}' - без заголовка.
2) В iOS есть фича, которая при шаринге подтягивает со страницы мета-информацию и в шапке попапа рисует
   картинку с заголовком. Фича крутая и важно её не потерять, и она перестает работать, если задан `text`.
2.1) Если передать `title` + `text` + `url`, то в шапке попапа будет виден `text`,
     в случае организации это ее адрес, скрин: https://nda.ya.ru/t/yMYUawME3W286c.
     После 'Copy' из попапа в буфере обмена окажется строчка '{text} {url}' - без заголовка.
2.2) А если передать `title` + `url`, то сначала в шапке отобразится хост (yandex.ru),
     скрин: https://nda.ya.ru/t/JPl795z63W287D, а спустя пару секунд подгрузится мета-информаниция
     и появится заголовок и картинка, скрин: https://nda.ya.ru/t/tOhAzMUZ3W287H.
     `title` при этом судя по всему не используется.

**Kind**: global constant  
<a name="addDirectWidgetScript"></a>

## addDirectWidgetScript() ⇒ <code>\*</code>
Добавляем скрипт виджета директа

**Kind**: global function  
<a name="assertViewCropViewport"></a>

## assertViewCropViewport()
Делает скриншот элемента, но только в пределе вьюпорта

**Kind**: global function  
<a name="clearCounters"></a>

## clearCounters() ⇒ <code>\*</code>
Очищаем объект со счётчиками

**Kind**: global function  
<a name="clickTo"></a>

## clickTo(selector, clientX, clientY) ⇒ <code>Promise</code>
Клик в определенную точку элемента

**Kind**: global function  

| Param | Type | Description |
| --- | --- | --- |
| selector | <code>String</code> | селектор элемента |
| clientX | <code>Number</code> | горизонтальный отступ от верхнего левого угла элемента selector |
| clientY | <code>Number</code> | вертикальный отступ от верхнего левого угла элемента selector |

<a name="closeOtherTabs"></a>

## closeOtherTabs() ⇒ <code>Promise</code>
Закрывает все открытые в браузере вкладки кроме первой

**Kind**: global function  
<a name="disableAnimation"></a>

## disableAnimation()
Отключает анимацию на всех блоках

**Kind**: global function  
<a name="disableStickyPlayer"></a>

## disableStickyPlayer(stickyContentSelector) ⇒ <code>\*</code>
Отлепляем плеер

**Kind**: global function  

| Param | Type | Description |
| --- | --- | --- |
| stickyContentSelector | <code>string</code> | селектор элемента |

<a name="enableExternalLinks"></a>

## enableExternalLinks(linksMode)
Управляет внешними ссылками на странице
Подробности тут: .templar/testing/assets/assets-hermione/common/no-external-links.js

**Kind**: global function  

| Param | Type | Description |
| --- | --- | --- |
| linksMode | <code>Boolean</code> \| <code>String</code> | режим работы ссылок |

<a name="enableInternalLinks"></a>

## enableInternalLinks(linksMode)
Управляет относительными ссылками на странице
Подробности тут: .templar/testing/assets/assets-hermione/common/no-external-links.js

**Kind**: global function  

| Param | Type | Description |
| --- | --- | --- |
| linksMode | <code>Boolean</code> \| <code>String</code> | режим работы ссылок |

<a name="fakeTimerTick"></a>

## fakeTimerTick(timeout, restore)
Делает тик фейкового таймера

**Kind**: global function  

| Param | Type | Default | Description |
| --- | --- | --- | --- |
| timeout | <code>Number</code> |  | время, на которое нужно промотать таймер |
| restore | <code>Boolean</code> | <code>true</code> | нужно ли обнулить счетчик, по умолчанию true |

<a name="focus"></a>

## focus() ⇒ <code>\*</code>
Чинит баг в firefox про неправильную работу keys
Подробности:
https://gitter.im/webdriverio/webdriverio?at=55f04dda5ba1e0ea6b804aca
https://gitter.im/webdriverio/webdriverio?at=55f0b62f24362d5253fe7c37

**Kind**: global function  
<a name="getCounter"></a>

## getCounter(counter, [timeout], [reverse]) ⇒ <code>Promise</code>
Возвращает параметры отправленного счётчика
Пробует каждые 100 ms получить этот счётчик в течение {timeout} или 1 секунды

Если вам нужно проверить, что счётчик не отправляется — используйте параметр reverse!

**Kind**: global function  

| Param | Type | Default | Description |
| --- | --- | --- | --- |
| counter | <code>Object</code> |  | Значения счётчика, по которым будет искаться вхождение в массиве mm.counters. Поддерживает regexp |
| [timeout] | <code>Number</code> | <code>1000</code> | сколько ждать в ms |
| [reverse] | <code>Boolean</code> |  | проверять, что счётчик не отправился |

<a name="getCounterByDecoded"></a>

## getCounterByDecoded(decoded, [timeout], [reverse]) ⇒ <code>Promise</code>
Ждет, пока в mm.counters появится счетчик с указанным decoded или совпадающий по regexp
Пробует каждые 200 получить этот счётчик в течение {timeout} или 1 секунды

**Kind**: global function  

| Param | Type | Default | Description |
| --- | --- | --- | --- |
| decoded | <code>Object</code> |  | Значение decoded счётчика к проверке или regexp |
| [timeout] | <code>Number</code> | <code>1000</code> | сколько ждать в ms |
| [reverse] | <code>Boolean</code> |  | проверять, что счётчик не отправился |

<a name="getCounterByName"></a>

## getCounterByName(name, [timeout], [reverse]) ⇒ <code>Promise</code>
Ждет, пока в mm.counters появится счетчик с указанным name
Пробует каждые 200 получить этот счётчик в течение {timeout} или 1 секунды

**Kind**: global function  

| Param | Type | Default | Description |
| --- | --- | --- | --- |
| name | <code>Object</code> |  | Значение name счётчика к проверке или regexp |
| [timeout] | <code>Number</code> | <code>1000</code> | сколько ждать в ms |
| [reverse] | <code>Boolean</code> |  | проверять, что счётчик не отправился |

<a name="getCounterByPath"></a>

## getCounterByPath(path, [timeout], [reverse]) ⇒ <code>Promise</code>
Ждет, пока в mm.counters появится счетчик с указанным path
Пробует каждые 200 получить этот счётчик в течение {timeout} или 1 секунды

**Kind**: global function  

| Param | Type | Default | Description |
| --- | --- | --- | --- |
| path | <code>Object</code> |  | Значение поля path счётчика к проверке или regexp |
| [timeout] | <code>Number</code> | <code>1000</code> | сколько ждать в ms |
| [reverse] | <code>Boolean</code> |  | проверять, что счётчик не отправился |

<a name="getPlayerFrame"></a>

## getPlayerFrame() ⇒ <code>Promise</code>
Возвращает html плеера

**Kind**: global function  
<a name="getPlayerFrameSrc"></a>

## getPlayerFrameSrc()
Возвращает html плеера

**Kind**: global function  
<a name="getPlayerId"></a>

## getPlayerId()
Возвращает playerId

**Kind**: global function  
<a name="getPlayerTestAttr"></a>

## getPlayerTestAttr()
Возвращает html плеера

**Kind**: global function  
<a name="getReduxStateValue"></a>

## getReduxStateValue(path) ⇒ <code>\*</code>
Достает из стейта Redux-стора значение по строковому пути, переданному в функцию
Бросает ошибку, если стора нет в глобальной переменной __reduxStore__
или если по указанному пути не найдено значение

**Kind**: global function  

| Param | Type |
| --- | --- |
| path | <code>String</code> | 

<a name="getReqId"></a>

## getReqId(element, [attr]) ⇒ <code>Promise</code>
Вытаскиваем ReqId из указанного элемента.

**Kind**: global function  

| Param | Type | Description |
| --- | --- | --- |
| element | <code>Object</code> | элемент хранящий на себе counter__reqid |
| [attr] | <code>String</code> | атрибут, в котором лежат параметры c полем reqid |

<a name="getScrollPosition"></a>

## getScrollPosition(element) ⇒ <code>Promise</code>
Получаем позицию скрола у скролируемой области

**Kind**: global function  

| Param | Type | Description |
| --- | --- | --- |
| element | <code>Object</code> | элемент, который можно сколлить |

<a name="getVideoData"></a>

## getVideoData(element) ⇒ <code>Promise</code>
Возвращает данные ролика из указанного элемента

**Kind**: global function  

| Param | Type | Description |
| --- | --- | --- |
| element | <code>Object</code> | элемент хранящий на себе данные ролика |

<a name="getViewerReqid"></a>

## getViewerReqid([reduxStatePath]) ⇒ <code>Promise</code>
Вытаскиваем reqid из состояния redux-хранилища,
если передан путь до объекта в сторе, содержащего поле reqid
Берем из начальных пропсов, если путь не передан

**Kind**: global function  

| Param | Type | Description |
| --- | --- | --- |
| [reduxStatePath] | <code>string</code> | из какого объекта redux-стора брать |

<a name="openSPASFromWeb4"></a>

## openSPASFromWeb4(urlOptions) ⇒ <code>Webdriverio</code>
Перед переходом на страницу сценария сначала открывает СЕРП с флагами SPAS.
После открытия СЕРПа происходит SPAS переход на адрес сценария.

**Kind**: global function  

| Param | Type | Description |
| --- | --- | --- |
| urlOptions | <code>Object</code> | адрес страницы |

<a name="goSPASURL"></a>

## goSPASURL(opts) ⇒ <code>Webdriverio</code>
Имитирует открытие урла с помощью библиотеки search-spa.
Переход на переданный URL произойдёт с помощью AJAX-перехода со страницы web4.

**Kind**: global function  

| Param | Type | Description |
| --- | --- | --- |
| opts | <code>Object</code> | объект в формате для либы urijs |

<a name="goURL"></a>

## goURL(opts) ⇒ <code>Webdriverio</code>
Переход по URL

**Kind**: global function  

| Param | Type | Description |
| --- | --- | --- |
| opts | <code>Object</code> | объект в формате для либы urijs |

<a name="loadNextVideoPage"></a>

## loadNextVideoPage(currentPage) ⇒ <code>\*</code>
Загружает новую страницу сниппетов для всех страниц Видео
(Морда, Поиск, Мои Видео)

**Kind**: global function  

| Param | Type | Description |
| --- | --- | --- |
| currentPage | <code>String</code> | название текущией страницы ('search'|'index') |

<a name="makeTransparent"></a>

## makeTransparent(selector, mode)
Делает элементы по селектору прозрачными

**Kind**: global function  

| Param | Type | Default | Description |
| --- | --- | --- | --- |
| selector | <code>String</code> |  | селектор, по которому будет создано css правило |
| mode | <code>Boolean</code> | <code>true</code> | true если надо создать правило, false если надо его удалить |

<a name="preparePageForScroll"></a>

## preparePageForScroll() ⇒ <code>\*</code>
Подготовка страницы к скроллу (скрытие шапки, включение скоролла)

**Kind**: global function  
<a name="reStubImage"></a>

## reStubImage() ⇒ <code>Promise.&lt;Boolean&gt;</code>
Меняет параметры mmui-png-stub

**Kind**: global function  
<a name="retryActionsByElemNotVisible"></a>

## retryActionsByElemNotVisible(retries, selector, action) ⇒ <code>Promise</code>
Метод, который позволяет циклично выполнять последовательные действия в браузере
пока не пропадёт заданный элемент. Действия необязательно должны производиться над элементом

**Kind**: global function  

| Param | Type | Description |
| --- | --- | --- |
| retries | <code>Number</code> | количество повторений действий |
| selector | <code>String</code> | селектор элемента |
| action | <code>function</code> | действия |

<a name="retryActionsByElemVisible"></a>

## retryActionsByElemVisible(retries, selector, action) ⇒ <code>Promise</code>
Метод, который позволяет циклично выполнять последовательные действия в браузере
пока не появится искомый элемент. Действия необязательно должны производиться над элементом

**Kind**: global function  

| Param | Type | Description |
| --- | --- | --- |
| retries | <code>Number</code> | количество повторений действий |
| selector | <code>String</code> | селектор искомого элемента |
| action | <code>function</code> | действия |

<a name="saveReqId"></a>

## saveReqId(stateObject, element, [attr]) ⇒ <code>Promise</code>
Сохраняем текущий ReqID элемента чтобы потом проверить что он изменился в waitForReqId

**Kind**: global function  

| Param | Type | Description |
| --- | --- | --- |
| stateObject | <code>Object</code> | объект в который можно сохранить текущее состояние reqid |
| element | <code>Object</code> | элемент хранящий на себе counter__reqid |
| [attr] | <code>String</code> | атрибут, в котором лежат параметры c полем reqid |

<a name="scrollIntoView"></a>

## scrollIntoView(element, [params]) ⇒ <code>Promise</code>
Насильно скроллим к элементу при помощи JS в браузере.

**Kind**: global function  

| Param | Type | Description |
| --- | --- | --- |
| element | <code>Object</code> | элемент к которому нужно подскроллить. |
| [params] | <code>Object</code> | дополнительные параметры |
| [params.offset] | <code>Number</code> | насколько ниже\выше нужно подскроллить (отрицательное значение = выше элемента) |
| [params.offsetElements] | <code>Array.&lt;String&gt;</code> | селекторы фиксированных элементов, которые могут перекрыть при подскролле |

<a name="sendPlayerEvent"></a>

## sendPlayerEvent(event, [data])
Инициирует отправку события плеера

**Kind**: global function  

| Param | Type | Description |
| --- | --- | --- |
| event | <code>string</code> | Название события |
| [data] | <code>object</code> | Данные события |

<a name="setPlayerTestAttr"></a>

## setPlayerTestAttr()
Возвращает html плеера

**Kind**: global function  
<a name="setReactInputValue"></a>

## setReactInputValue() ⇒ <code>Promise</code>
Имитирует очистку инпута нажатиями кнопки BACKSPACE, а затем записывает строку в инпут
Обычный setValue не подойдет, т.к. встроенная в этот метод очистка не работает
React слушает событие изменения значения инпута, которое не триггерится при очистке

**Kind**: global function  
<a name="tickPlayerTimer"></a>

## tickPlayerTimer(timeout)
Делает тик таймера в песочнице

**Kind**: global function  

| Param | Type | Description |
| --- | --- | --- |
| timeout | <code>Number</code> | время, на которое нужно промотать таймер |

<a name="waitForImagesLoaded"></a>

## waitForImagesLoaded(selector) ⇒ <code>Promise</code>
Ожидает пока загрузятся картинки, удовлетворяющие заданному селектору

**Kind**: global function  

| Param | Type | Description |
| --- | --- | --- |
| selector | <code>string</code> | селектор картинок |

<a name="waitForItemLoaded"></a>

## waitForItemLoaded(selector) ⇒ <code>Promise</code>
Ожидает пока загрузится/перезагрузится указанный элемент выдачи

Ожидает элемент выдачи, у которого не стоит атрибут loaded=yes, после загрузки устанавливает его
Соответственно, если к элементу уже был вызов функции, то последующий вызов не зарезолвится
до тех пор, пока страница не будет перезагружена или выдача не перестроиться

**Kind**: global function  

| Param | Type | Description |
| --- | --- | --- |
| selector | <code>String</code> | селектор элемента выдачи, например PO.serpList.serpItem0()/PO.relatedVideo.relatedItem0() |

<a name="waitForAbsent"></a>

## waitForAbsent(selectors, options) ⇒ <code>Promise</code>
Функция позволяет дождаться,
пока элемент пропадёт,
если он в текущий момент присутствует на странице.

**Kind**: global function  

| Param | Type | Description |
| --- | --- | --- |
| selectors | <code>Array</code> | массив селекторов. |
| options | <code>Object</code> | объект параметров. |
| options.timeout | <code>number</code> | timeout в милисекундах на ожидание элемента. |

<a name="waitForLoad"></a>

## waitForLoad() ⇒ <code>\*</code>
Ожидаем когда пропадет fade и появится .b-page_js_inited для выдачи и #root.root_inited для просмотрщика

**Kind**: global function  
<a name="waitForNewTab"></a>

## waitForNewTab([timeout], [reverse]) ⇒ <code>Promise</code>
Ожидаем когда будет открыта новая вкладка(ки)
Проверяем на количество активных вкладок каждые 200 мс в течении {timeout} или 3 секунд

**Kind**: global function  

| Param | Type | Description |
| --- | --- | --- |
| [timeout] | <code>Number</code> | сколько ждать в ms |
| [reverse] | <code>Boolean</code> | проверять, что новая вкладка не открылась |

<a name="waitForPlayerLoaded"></a>

## waitForPlayerLoaded([timeout]) ⇒ <code>Promise</code>
Ожидает загрузки стаба плеера

**Kind**: global function  

| Param | Type | Description |
| --- | --- | --- |
| [timeout] | <code>Number</code> | Таймаут в миллисекундах |

<a name="waitForReqIdToChange"></a>

## waitForReqIdToChange(stateObject, element, [options]) ⇒ <code>Promise</code>
Проверяем текущий ReqID элемента сравнивая его с сохраненным в saveReqId

**Kind**: global function  

| Param | Type | Description |
| --- | --- | --- |
| stateObject | <code>Object</code> | объект в котором сохранено состояние reqid |
| element | <code>Object</code> | элемент хранящий на себе counter__reqisd |
| [options] | <code>Object</code> | дополнительные опции |
| [options.reverse] | <code>Boolean</code> | инвертировать проверку (проверять что НЕ поменялся) |
| [options.attr] | <code>String</code> | атрибут, в котором лежат параметры с полем reqid |
| [options.timeout] | <code>Number</code> | таймаут ожидания |

<a name="waitForSrcToChange"></a>

## waitForSrcToChange(stateObject, element, [options], [timeoutMsg]) ⇒ <code>Promise</code>
Проверяем текущий src элемента сравнивая его с сохраненным ранее (в saveSrc?)

**Kind**: global function  

| Param | Type | Description |
| --- | --- | --- |
| stateObject | <code>Object</code> | объект в котором сохранено предыдущее состояние src |
| element | <code>Object</code> | элемент, на котором нужно взять src |
| [options] | <code>Object</code> | дополнительные параметры |
| [options.ignoreThumbs] | <code>Boolean</code> | игнорировать простановку тумбов в src |
| [options.regexp] | <code>RegExp</code> | RegExp, которому должен соответствовать src |
| [options.reverseRE] | <code>Boolean</code> | reverse RegExp'а |
| [options.timeout] | <code>Number</code> | таймаут ожидания |
| [timeoutMsg] | <code>Number</code> | сообщение об ошибке |

<a name="waitForUrl"></a>

## waitForUrl(predicate, msg) ⇒ <code>Promise</code>
Ожидание условия в текущем URL.
Есть баг в webdriver. Если не указать msg, ничего не будет работать.

**Kind**: global function  

| Param | Type | Default | Description |
| --- | --- | --- | --- |
| predicate | <code>function</code> |  | Условие, которое должно выполниться |
| msg | <code>String</code> | <code>URL не изменился</code> | Сообщение, которое прокидывается в assert |

<a name="yaApiClearCallHistory"></a>

## yaApiClearCallHistory() ⇒ <code>Promise</code>
Очищает историю вызовов методов YandexAppsAPI

**Kind**: global function  
<a name="yaCheckApiOpenRelatedQuery"></a>

## yaCheckApiOpenRelatedQuery(params, [timeout]) ⇒ <code>Promise</code>
Проверка работы метода API openRelatedQuery

**Kind**: global function  

| Param | Type | Description |
| --- | --- | --- |
| params | <code>object</code> | параметры вызова метода |
| params.query | <code>string</code> | текст запроса |
| params.url | <code>string</code> | ссылка для перезапроса |
| [timeout] | <code>Number</code> | таймаут в миллисекундах |

<a name="yaCheckCanonical"></a>

## yaCheckCanonical() ⇒ <code>Promise</code>
Проверка canonical-ссылки. Возвращает текущий url и каноническую ссылку

**Kind**: global function  
<a name="yaCheckClientCounter"></a>

## yaCheckClientCounter() ⇒ <code>Promise</code>
Проверяет срабатывание клиентских счетчиков (они же счетчики действий, они же редир-счетчики) по редир-логу
Если рекид не задан, то выполняется фоллбек на глобальный рекид страницы
Это сработает, например, если проверяется счетчик для картинки с первой страницы выдачи

- @param {String} reqid - рекид счетчика
- @param {CounterObject|CounterObject[]} expected - Клиентские счётчики (счётчик), которые должны сработать
- @param {String} [message] - Сообщение, если счётчик не сработал
- @param {CounterOptions} [options]

options.shouldNotBeTriggered - проверяет, что счетчик не был вызван.

**Kind**: global function  
<a name="yaCheckDeeplink"></a>

## yaCheckDeeplink(selector, [message], noFallback) ⇒ <code>Promise</code>
**Kind**: global function  

| Param | Type | Default | Description |
| --- | --- | --- | --- |
| selector | <code>String</code> |  |  |
| [message] | <code>String</code> | <code>Диплинк на ссылке не обнаружен</code> | кастомное базовое сообщение об ошибке,   которое будет дополнено информацией о конкретной ошибке |
| noFallback | <code>Object</code> |  | Флаг, выключающий проверку фолбека, потому что в некоторых кейсах фолбек не нужен. |

<a name="yaCheckLinkOpener"></a>

## yaCheckLinkOpener(selector, [message], [params]) ⇒ <code>Promise.&lt;Url&gt;</code>
Команда для базовых проверок ссылки

1. Атрибут href ссылки не пуст и не состоит из пробельных символов
2. Ссылка открывается с правильным атрибутом 'target'
3. По ссылке можно кликнуть

**Kind**: global function  
**Returns**: <code>Promise.&lt;Url&gt;</code> - - разобранный URL  

| Param | Type | Default | Description |
| --- | --- | --- | --- |
| selector | <code>String</code> |  |  |
| [message] | <code>String</code> | <code>Параметры ссылки содержат неверные значения</code> | кастомное базовое сообщение об ошибке,   которое будет дополнено информацией о конкретной ошибке |
| [params] | <code>Object</code> |  |  |
| [params.target] | <code>String</code> | <code>_blank|_self</code> | открывать ссылку в новой вкладке/оставаться в текущей вкладке |
| [params.clickCoords] | <code>Array</code> |  | координаты клика, есть надо кликать не в центр элемента |

<a name="yaCheckPassportUrl"></a>

## yaCheckPassportUrl() ⇒ <code>Promise</code>
Проверка ссылки перехода на паспорт

**Kind**: global function  
**Params**: <code>String</code> selector - Селектор элемента  
**Params**: <code>String</code> passportUrl - подстрока ссылки для перехода на паспорт, например //passport.yandex.ru/auth  
**Params**: <code>?String</code> origin - origin параметр, передаваемый в ссылку  
<a name="yaCheckServerCounter"></a>

## yaCheckServerCounter() ⇒ <code>Promise</code>
Проверяет срабатывание серверных счетчиков (они же блокстат-счетчики, они же счетчики показа) по блокстат-логу

- @param {String} reqid
- @param {CounterObject|CounterObject[]} expected - Серверные счётчики (счётчик), которые должны сработать
- @param {String} [message] - Сообщение, если счётчик не сработал
- @param {CounterOptions} [options]

**Kind**: global function  
<a name="yaCheckText"></a>

## yaCheckText() ⇒ <code>Promise</code>
Проверка текста, содержащегося в элементе

**Kind**: global function  
**Params**: <code>String</code> selector - Селектор элемента  
**Params**: <code>String</code> text - Текст  
<a name="yaCheckURL"></a>

## yaCheckURL(actualUrl, expectedUrl, [message], [params])
Команда для проверки URL

**Kind**: global function  

| Param | Type | Default | Description |
| --- | --- | --- | --- |
| actualUrl | <code>Object</code> \| <code>String</code> |  | Cравниваемый URL |
| expectedUrl | <code>Object</code> \| <code>String</code> |  | Ожидаемый URL |
| [expectedUrl.queryValidator] | <code>function</code> |  | Кастомный валидатор параметров |
| [expectedUrl.url] | <code>String</code> |  | Ожидаемый URL |
| [message] | <code>String</code> | <code>Ошибочный адрес</code> | Кастомное базовое сообщение об ошибке,   которое будет дополнено информацией о конкретной ошибке |
| [params] | <code>Object</code> |  |  |
| [params.skipProtocol] | <code>Boolean</code> | <code>false</code> | Отключить проверку протокола |
| [params.skipHostname] | <code>Boolean</code> | <code>false</code> | Отключить проверку hostname |
| [params.skipPathname] | <code>Boolean</code> | <code>false</code> | Отключить проверку pathname |
| [params.skipQuery] | <code>Boolean</code> | <code>false</code> | Отключить проверку параметров запроса |
| [params.skipHash] | <code>Boolean</code> | <code>false</code> | Отключить проверку hash |

<a name="yaChooseCbirFile"></a>

## yaChooseCbirFile(filePath) ⇒ <code>Promise</code>
Загружает файл в поиск по картинке (Сибирь) через кнопку фотоаппарата в стрелке

**Kind**: global function  

| Param | Type | Description |
| --- | --- | --- |
| filePath | <code>String</code> | Путь к загружаемому файлу |

<a name="yaCleanSessionStorage"></a>

## yaCleanSessionStorage(storageKey) ⇒ <code>Promise</code>
Команда для очистки sessionStorage

**Kind**: global function  

| Param | Type | Description |
| --- | --- | --- |
| storageKey | <code>String</code> | ключ для очистки |

<a name="yaClearImagesFilter"></a>

## yaClearImagesFilter()
Сбрасывает активные фильтры сервиса Картинки

**Kind**: global function  
<a name="yaCloseDirect"></a>

## yaCloseDirect(selector)
Эмуляция закрытия блока директа

**Kind**: global function  

| Param | Type | Description |
| --- | --- | --- |
| selector | <code>String</code> | селектор блока директа |

<a name="yaCloseMiniSuggest"></a>

## yaCloseMiniSuggest()
Закрывает саджест (mini-suggest)
В некоторых сценариях оверлей mini-suggest__overlay ломает тесты, если его не закрыть
Возвращает промис по закрытию оверлея

**Kind**: global function  
<a name="yaCloseSafariTabs"></a>

## yaCloseSafariTabs() ⇒ <code>Promise</code>
Закрывает лишние открытые табы при выполнении теста в мобильном safari.
TODO: использовать плагин hermione-tabs-closer после - https://st.yandex-team.ru/FEI-24830

**Kind**: global function  
<a name="yaExecuteInFrame"></a>

## yaExecuteInFrame(actions, iframeSelector)
переключает на контекст iframe коллекций и
выполняет указанные действия

**Kind**: global function  

| Param | Type | Description |
| --- | --- | --- |
| actions | <code>function</code> | действия |
| iframeSelector | <code>function</code> | селектор iframe |

<a name="normalizeExpectationsResults"></a>

## normalizeExpectationsResults()
Нормализует результаты "expectation"-ов

**Kind**: global function  
<a name="yaExpectOnPage"></a>

## yaExpectOnPage(config, [timeout]) ⇒ <code>Promise</code>
Выполняет проверки сразу после загрузки страницы

**Kind**: global function  

| Param | Type | Default | Description |
| --- | --- | --- | --- |
| config | <code>ExpectationsConfig</code> |  | Конфигурация обязательных проверок, исполняемых в контексте браузера |
| [timeout] | <code>Number</code> | <code>10000</code> | Время ожидания загрузки страницы в миллисекундах |

<a name="yaExtendArea"></a>

## yaExtendArea() ⇒ <code>\*</code>
Расширяем зону снимка вокруг выбранного блока

**Kind**: global function  
<a name="yaForceRelativePosition"></a>

## yaForceRelativePosition(selector) ⇒ <code>Promise.&lt;DOMRect&gt;</code>
Проставляет элементу position: relative.
Данную команду надо применять для элементов с position: fixed или sticky,
чтобы на скриншотах не было дублирование.

**Kind**: global function  

| Param | Type | Description |
| --- | --- | --- |
| selector | <code>Object</code> | Селектор элемента |

<a name="yaGetAttributes"></a>

## yaGetAttributes(selector, attributeName) ⇒ <code>Promise.&lt;Array.&lt;String&gt;&gt;</code>
Получить значения атрибута для DOM-элементов.

Отличия от существующего getAttribute(selector, attributeName):
- не генерирует ошибку, если не находит ни одного элемента по селектору
- всегда возвращает массив (getAttribute возвращает строку, если находит только один элемент)

**Kind**: global function  

| Param | Type | Description |
| --- | --- | --- |
| selector | <code>String</code> | Селектор элементов |
| attributeName | <code>String</code> | Название атрибута |

<a name="yaGetBoundingClientRect"></a>

## yaGetBoundingClientRect(selector) ⇒ <code>Promise.&lt;DOMRect&gt;</code>
Получает геометрию элемента на странице

**Kind**: global function  

| Param | Type | Description |
| --- | --- | --- |
| selector | <code>String</code> | Селектор элемента |

<a name="yaGetCbirCropRect"></a>

## yaGetCbirCropRect()
Получает геометрию элемента на странице

**Kind**: global function  
<a name="yaGetComputedStyle"></a>

## yaGetComputedStyle(selector) ⇒ <code>Promise.&lt;CSSStyleDeclaration&gt;</code>
Получает все значения CSS свойств элементов после применения стилей

**Kind**: global function  

| Param | Type | Description |
| --- | --- | --- |
| selector | <code>String</code> | Селектор элемента |

<a name="yaGetDirectId"></a>

## yaGetDirectId(selector)
Получение площадки блока директа

**Kind**: global function  

| Param | Type | Description |
| --- | --- | --- |
| selector | <code>String</code> | селектор блока директа |

<a name="yaGetElementIndex"></a>

## yaGetElementIndex(selector) ⇒ <code>Number</code>
Возвращает индекс элемента в списке соседних нод для своей родительской ноды

**Kind**: global function  

| Param | Type | Description |
| --- | --- | --- |
| selector | <code>String</code> | Селектор DOM ноды |

<a name="yaGetGlobalParam"></a>

## yaGetGlobalParam(key) ⇒ <code>Promise</code>
Возвращает значение параметра в блоке i-global

**Kind**: global function  

| Param | Type | Description |
| --- | --- | --- |
| key | <code>String</code> | имя параметра |

<a name="yaGetInlineStyle"></a>

## yaGetInlineStyle(selector) ⇒ <code>Promise.&lt;CSSStyleDeclaration&gt;</code>
Получает все значения инлайновых CSS свойств элемента

**Kind**: global function  

| Param | Type | Description |
| --- | --- | --- |
| selector | <code>String</code> | Селектор элемента |

<a name="yaGetTexts"></a>

## yaGetTexts(selector) ⇒ <code>Promise.&lt;Array.&lt;String&gt;&gt;</code>
Получить текст всех найденных DOM-элементов.

Отличия от существующего getText(selector):
- ищет текст у всех найденных DOM-элементов, а не только для первого
- возвращает текст даже для скрытых элементов

**Kind**: global function  

| Param | Type | Description |
| --- | --- | --- |
| selector | <code>String</code> | Селектор элементов |

<a name="yaHideDeviceKeyboard"></a>

## yaHideDeviceKeyboard()
Прячет клавиатуру только для тех браузеров, которые это умеют

**Kind**: global function  
<a name="yaHideElements"></a>

## yaHideElements(selectors, [mode]) ⇒ <code>Promise</code>
Скрывает элементы по селекторам

**Kind**: global function  

| Param | Type | Default | Description |
| --- | --- | --- | --- |
| selectors | <code>Array.&lt;string&gt;</code> |  | Список селекторов |
| [mode] | <code>&#x27;display&#x27;</code> \| <code>&#x27;visibility&#x27;</code> \| <code>&#x27;opacity&#x27;</code> | <code>&#x27;display&#x27;</code> | Режим скрытия |

<a name="yaInjectStyle"></a>

## yaInjectStyle()
Объявляет переданный стиль для переданного селектора

**Kind**: global function  
<a name="yaKeyPress"></a>

## yaKeyPress(codes) ⇒ <code>Promise</code>
Управление клавиатурой

**Kind**: global function  

| Param | Type | Description |
| --- | --- | --- |
| codes | <code>String</code> | Код клавиши |

<a name="yaMiniSuggestClick"></a>

## yaMiniSuggestClick(selector, [retry]) ⇒ <code>Promise</code>
Клик в элемент mini-suggest на тачах после появления саджеста.
В mini-suggest'е на тачах при открытии саджеста происходит фриз кликов на 500мс,
из-за этого тесты моргают тесты моргают
https://a.yandex-team.ru/arc_vcs/frontend/packages/mini-suggest/touch.blocks/mini-suggest/mini-suggest.js?rev=be27f8e3585169a94f28f418c6f95a5d8e953b54#L21

**Kind**: global function  

| Param | Type | Default | Description |
| --- | --- | --- | --- |
| selector | <code>String</code> |  | селектор элемента |
| [retry] | <code>Number</code> | <code>3</code> | количество попыток |

<a name="yaMockXHR"></a>

## yaMockXHR(options)
jsdoc для удобства взят из файла .config/templar/testing/assets/assets-hermione/common/mockXHR.js

Функция для организации стабов/моков аяксовых запросов.
Реализована с помощью подмены оригинального метода open из XMLHttpRequest
Перехватывает запросы по подходящим урлам (задаются в опциях) и отдаёт необходимые данные без сетевого запроса
Все остальные запросы осуществляются как обычно

**Kind**: global function  

| Param | Type | Description |
| --- | --- | --- |
| options | <code>Object</code> | параметры перехвата запросов |
| options.status | <code>Number</code> | имитируемый код ответа (по умолчанию 200) |
| options.urlDataMap | <code>Record.&lt;String, any&gt;</code> | хеш,      ключи — строки-регулярные выражения для поиска совпадающего урла (например, ^https?://yabs.yandex.ru/page/[0-9]+)      значение — замоканый ответ сервера. Если будет передана не строка, то значение будет конвертировано в строку с          помощью JSON.stringify |
| options.urlRedirectMap | <code>Record.&lt;String, String&gt;</code> | хеш редиректов,      ключи — строки-регулярные выражения для поиска совпадающего урла (например, ^https?://yabs.yandex.ru/page/[0-9]+)      значение — строка для применения в функции <String>.replace |
| options.recordData | <code>Array.&lt;String&gt;</code> | массив урлов, запросы по которым нужно отслеживать      Собирает объект параметров запроса в window['hermione-mock-xhr-records']      элементы — строки-регулярные выражения для поиска совпадающего урла |

<a name="yaMoveAndClick"></a>

## yaMoveAndClick(selector, x, y) ⇒ <code>Promise</code>
Клик в элемент по координатам.
(т.к. leftClick не работает в FF)

**Kind**: global function  

| Param | Type | Description |
| --- | --- | --- |
| selector | <code>String</code> | Селектор элемента |
| x | <code>Number</code> | Координата x |
| y | <code>Number</code> | Координата y |

<a name="yaOpenImageViewer"></a>

## yaOpenImageViewer(options)
Функция для открытия просмотрщика картинок

**Kind**: global function  

| Param | Type | Description |
| --- | --- | --- |
| options | <code>Object</code> | параметры открытия просмотрщика |
| options.open | <code>Object</code> | параметры открытия страницы (соответствует формату query в goURL)      Можно передать false, если нужная страница уже открыта, и открывать не нужно. В этом случае      параметры mock применены не будут |
| options.mock | <code>Object</code> | параметры стабов аяксовых запросов в просмотрщике.              По умолчанию, стабит пустыми ответами утку, рим и рекламу (этих элементов по умолчанию не будет) |
| options.serpItem | <code>String</code> | селектор серп-айтема, на который нужно кликнуть для открытия просмотрщика      По умолчанию — первый серпайтем |
| options.targetFeature | <code>Object</code> | целевая фича, появление которой нужно дождаться.      Например, дождаться отрисовки директного сниппета |

<a name="yaOpenImagesFilter"></a>

## yaOpenImagesFilter()
Отображает список фильтров сервиса Картинки, если он скрыт

**Kind**: global function  
<a name="yaOpenPageAndWaitSelector"></a>

## yaOpenPageAndWaitSelector(options) ⇒ <code>Promise</code>
Открывает заданную страницу с параметрами и дожидается отображения элемента на странице

**Kind**: global function  

| Param | Type | Description |
| --- | --- | --- |
| options | <code>Object</code> | Селектор для элемента, появление которого нужно ждать |
| options.page | <code>YaPage</code> | Идентификатор страницы |
| options.selector | <code>String</code> | QuerySelector ожидаемого элемента |
| [options.query] | <code>Object</code> | Параметры запроса |
| [options.errorMessage] | <code>String</code> | Кастомный тескт ошибки |

<a name="yaParseUrl"></a>

## yaParseUrl() ⇒ <code>Promise.&lt;Url&gt;</code>
Получить и распарсить текущий URL

**Kind**: global function  
<a name="yaPassportLogin"></a>

## yaPassportLogin(PO, login, password) ⇒ <code>Promise</code>
Хелпер для быстрой авторизации в паспорте

**Kind**: global function  

| Param | Type |
| --- | --- |
| PO | <code>Object</code> | 
| login | <code>String</code> | 
| password | <code>String</code> | 

<a name="yaPatchResponse"></a>

## yaPatchResponse(params)
Патч для ответов XmlHttpRequest.

Если нужно успеть перехватить запросы при загрузке страницы,
то нужно добавить в desiredCapabilities поле pageLoadStrategy='none'.
Тогда goURL не будет ждать события load.

**Kind**: global function  

| Param | Type |
| --- | --- |
| params | <code>Object</code> | 
| params.matcher | <code>String</code> \| <code>function</code> | 
| params.patcher | <code>function</code> | 

**Example**  
```js
this.browser
  .goURL({path: '/video/tvapp/'})
  .yaPatchResponse({
    matcher: 'carousels_videohub.json',
    patcher: data => {
      data.userId = 'foo';
      return data;
    }
  })
```
<a name="yaPauseAjaxStubs"></a>

## yaPauseAjaxStubs(paused)
Приостанавливает или возобновляет все ajax стабы

**Kind**: global function  

| Param | Type | Description |
| --- | --- | --- |
| paused | <code>boolean</code> | Признак приостановленности ajax запросов |

<a name="yaRemoveLocalStorageItem"></a>

## yaRemoveLocalStorageItem(keyName)
Удаляет запись из localStorage по имени ключа

**Kind**: global function  

| Param | Type | Description |
| --- | --- | --- |
| keyName | <code>string</code> | имя ключа в localStorage |

<a name="yaScroll"></a>

## yaScroll(selector, alignToTop)
Скролит вьюпорт к нужному элементу

**Kind**: global function  

| Param | Default | Description |
| --- | --- | --- |
| selector |  | селектор, который должен попасть в зону видимости |
| alignToTop | <code>true</code> | прокрутить так, чтобы элемент был выровнен с вьюпортом по верхнему краю (по-умолчанию, true) |

<a name="yaScrollContainerToElem"></a>

## yaScrollContainerToElem(elem, container) ⇒ <code>Promise</code>
Скролит родителя к указанному дочернему элементу

**Kind**: global function  

| Param | Type | Description |
| --- | --- | --- |
| elem | <code>string</code> | дочерний элемент |
| container | <code>string</code> | родительский элемент |

<a name="yaScrollElement"></a>

## yaScrollElement(selector, top, left)
Скролит элемент на указанное количество пикселей

**Kind**: global function  

| Param | Description |
| --- | --- |
| selector | селектор |
| top | количество пикселей для свойства scrollTop |
| left | количество пикселей для свойства scrollLeft |

<a name="yaScrollPage"></a>

## yaScrollPage(value)
Скролит страницу на указанное количесвто пикселей с учетом особенностей браузеров грида

**Kind**: global function  

| Param | Description |
| --- | --- |
| value | количество пикселей |

<a name="yaScrollPageToBottom"></a>

## yaScrollPageToBottom()
Скролит страницу, пока не достигнет её конца.
Это нужно для тех случаев, когда на странице есть блоки, которые по скроллу добавляют на страницу контент.

**Kind**: global function  
<a name="yaSetGlobalParam"></a>

## yaSetGlobalParam(key, value) ⇒ <code>Promise</code>
Устанавливает значение параметра в блоке i-global

**Kind**: global function  

| Param | Type | Description |
| --- | --- | --- |
| key | <code>String</code> | имя параметра |
| value | <code>\*</code> | значение параметра |

<a name="yaSetLocalStorageItem"></a>

## yaSetLocalStorageItem(key, value)
Добаляет запись в localStorage

**Kind**: global function  

| Param | Type | Description |
| --- | --- | --- |
| key | <code>string</code> | имя ключа в localStorage |
| value | <code>string</code> | значение ключа в localStorage |

<a name="yaShouldBeSame"></a>

## yaShouldBeSame(s1, s2, [message]) ⇒ <code>Boolean</code>
Проверяет что два селектора указывает на один и тот же узел

**Kind**: global function  

| Param | Type | Description |
| --- | --- | --- |
| s1 | <code>String</code> |  |
| s2 | <code>String</code> |  |
| [message] | <code>String</code> | Сообщение об ошибке |

<a name="yaShouldBeSizeable"></a>

## yaShouldBeSizeable(selector, [message]) ⇒ <code>Promise.&lt;Boolean&gt;</code>
Проверяет что элемент имеет ненулевой размер

**Kind**: global function  

| Param | Type | Description |
| --- | --- | --- |
| selector | <code>String</code> | Селектор элемента |
| [message] | <code>String</code> | Читаемое название элемента |

<a name="yaShouldBeVisible"></a>

## yaShouldBeVisible(selector, [message]) ⇒ <code>Promise.&lt;Boolean&gt;</code>
Проверяет, что элемент видим в данный момент. Если показа не нужно ждать, лучше использовать yaShouldBeVisible,
а не waitForVisible. Если по селектору выберется несколько элементов, выбросит ошибку.

**Kind**: global function  

| Param | Type | Description |
| --- | --- | --- |
| selector | <code>String</code> | Селектор элемента |
| [message] | <code>String</code> | Сообщение об ошибке |

<a name="yaShouldBeVisibleWithinViewport"></a>

## yaShouldBeVisibleWithinViewport(selector, [message]) ⇒ <code>Promise.&lt;Boolean&gt;</code>
Проверяет, что элемент видим и находится в пределах вьюпорта.
Если по селектору выберется несколько элементов, выбросит ошибку.

**Kind**: global function  

| Param | Type | Description |
| --- | --- | --- |
| selector | <code>String</code> | Селектор элемента |
| [message] | <code>String</code> | Сообщение об ошибке |

<a name="yaShouldExist"></a>

## yaShouldExist(selector, [message]) ⇒ <code>Promise.&lt;Boolean&gt;</code>
Проверяет, что элемент существует на странице в данный момент.
Если появления ноды в DOM не нужно ждать, лучше использовать yaShouldExist, а не waitForExist

**Kind**: global function  

| Param | Type | Description |
| --- | --- | --- |
| selector | <code>String</code> | Селектор элемента |
| [message] | <code>String</code> | Сообщение об ошибке |

<a name="yaShouldNotBeVisible"></a>

## yaShouldNotBeVisible(selector, message) ⇒ <code>Promise.&lt;Boolean&gt;</code>
Проверяет, что элемент невидим/отсутствует в данный момент.
Если скрытия не нужно ждать, лучше использовать yaShouldNotBeVisible, а не yaWaitForHidden.
Если по селектору выберется несколько элементов, выбросит ошибку.

**Kind**: global function  

| Param | Type | Description |
| --- | --- | --- |
| selector | <code>String</code> | Селектор элемента |
| message | <code>String</code> | Кастомное сообщение об ошибке |

<a name="yaShouldNotExist"></a>

## yaShouldNotExist(selector, [message]) ⇒ <code>Promise.&lt;Boolean&gt;</code>
Проверяет, что элемент отсутствует на странице в данный момент.

**Kind**: global function  

| Param | Type | Description |
| --- | --- | --- |
| selector | <code>String</code> | Селектор элемента |
| [message] | <code>String</code> | Сообщение об ошибке |

<a name="yaShowAquar"></a>

## yaShowAquar() ⇒ <code>Promise.&lt;Boolean&gt;</code>
Выводит ссылки на сессии из Аквар (https://nerevar.at.yandex-team.ru/611), не все сессии лежат в одной табличке,
поэтому тут несколько ссылок, в них есть метрики и все счётчики которые были вызваны на сервере и клиенте

**Kind**: global function  
<a name="yaSimulatedMouseDrag"></a>

## yaSimulatedMouseDrag(selector, onX, onY) ⇒ <code>Promise</code>
Выполняет перетаскивание элемента мышью на заданное значение X и Y.
Последовательно генерирует 3 события: mousedown, mousemove, mouseup.
Начальной точкой перетаскивания является центр DOMRect элемента.

**Kind**: global function  

| Param | Type | Description |
| --- | --- | --- |
| selector | <code>String</code> | Селектор DOM ноды, на которой нужно начать перетаскивание |
| onX | <code>Number</code> | Сдвиг по оси X |
| onY | <code>Number</code> | Сдвиг по оси Y |

<a name="yaSimulatedSwipe"></a>

## yaSimulatedSwipe(selector, onX, onY, inAnimationFrame) ⇒ <code>Promise</code>
Выполняет свайп на заданное значение X и Y.
Последовательно генерирует 3 события: touchstart, touchmove, touchend.
Начальной точкой свайпа является центр DOMRect элемента.

**Kind**: global function  

| Param | Type | Description |
| --- | --- | --- |
| selector | <code>String</code> | Селектор DOM ноды, на которой нужно начать свайп |
| onX | <code>Number</code> | Сдвиг по оси X |
| onY | <code>Number</code> | Сдвиг по оси Y |
| inAnimationFrame | <code>Boolean</code> | тригерим события на requestAnimationFrame |

<a name="yaStubBeforeUnloadEvents"></a>

## yaStubBeforeUnloadEvents(enabled)
Устанавливает или снимает stub на BeforeUnloadEvent события.
Для установки стаба нужно передать true в enables, для снятия - false.

**Kind**: global function  

| Param | Type | Default | Description |
| --- | --- | --- | --- |
| enabled | <code>boolean</code> | <code>true</code> | включить (true) или выключить (false) стаб, по умолчанию true |

<a name="yaToggleCssTransitions"></a>

## yaToggleCssTransitions(enabled) ⇒ <code>\*</code>
Включает анимации, отключённые в гермионе по умолчанию

**Kind**: global function  

| Param | Type | Description |
| --- | --- | --- |
| enabled | <code>boolean</code> | Признак активности анимаций |

<a name="yaTouch"></a>

## yaTouch(selector, forceClickPlatforms) ⇒ <code>Promise</code>
Тач клик на элемент

**Kind**: global function  
**Copypaste**: https://a.yandex-team.ru/arc_vcs/frontend/projects/web4/hermione/commands/commands-generic/common/yaTouch.js?rev=65f44395e3d0207e583155524fb72e4e6a9ca5de  

| Param | Type | Description |
| --- | --- | --- |
| selector | <code>String</code> |  |
| forceClickPlatforms | <code>Array</code> | плафтормы для которых по-умолчанию вызываем click |

<a name="yaUnpinHeader"></a>

## yaUnpinHeader()
Отключает залипание шапки для тестов

**Kind**: global function  
<a name="yaUnstubViewerCbirUrl"></a>

## yaUnstubViewerCbirUrl() ⇒ <code>Promise.&lt;Boolean&gt;</code>
Убирает ссылку на заглушку с кнопки поиска по картинке

**Kind**: global function  
<a name="yaWaitForAttributeChange"></a>

## yaWaitForAttributeChange(selector, attr, prevValue) ⇒ <code>Promise.&lt;string&gt;</code>
Ожидает пока поменяется атрибут у элемента.

**Kind**: global function  

| Param | Type | Description |
| --- | --- | --- |
| selector | <code>string</code> | селектор элемента |
| attr | <code>string</code> | имя атрибута |
| prevValue | <code>string</code> | предыдущее значение атрибута |

<a name="yaWaitForCbirId"></a>

## yaWaitForCbirId() ⇒ <code>Promise.&lt;Boolean&gt;</code>
Ждёт появления cbir_id в урле страницы

**Kind**: global function  
<a name="yaWaitForCbirOriginalImageUrl"></a>

## yaWaitForCbirOriginalImageUrl() ⇒ <code>Promise.&lt;Boolean&gt;</code>
Ждёт появления url в урле страницы

**Kind**: global function  
<a name="yaWaitForComputedStyle"></a>

## yaWaitForComputedStyle(selector, source, [message]) ⇒ <code>Promise</code>
Ждёт изменение CSS свойств элемента

**Kind**: global function  

| Param | Type | Default | Description |
| --- | --- | --- | --- |
| selector | <code>String</code> |  | Селектор элемента |
| source | <code>Object</code> \| <code>function</code> |  | Объект для сравнения стилей или функция-предикат |
| [message] | <code>String</code> | <code>CSS-свойства не изменились</code> | Сообщение об ошибке |

<a name="yaWaitForHidden"></a>

## yaWaitForHidden(selector, [timeout], [message]) ⇒ <code>Promise</code>
Обёртка над стандартной командой waitForVisible. Позволяет указывать произвольное сообщение об ошибке.
Чтобы дождаться скрытия элемента webdriver.io предлагает использовать waitForVisible(selector, timeout, true),
что выглядит непонятно.

**Kind**: global function  

| Param | Type | Description |
| --- | --- | --- |
| selector | <code>String</code> | Селектор для элемента, появление которого нужно ждать |
| [timeout] | <code>Number</code> | Таймаут в миллисекундах |
| [message] | <code>String</code> | Сообщение об ошибке |

<a name="yaWaitForInlineStyle"></a>

## yaWaitForInlineStyle(selector, source, [message]) ⇒ <code>Promise</code>
Ждёт изменение инлайновых CSS свойств элемента

**Kind**: global function  

| Param | Type | Default | Description |
| --- | --- | --- | --- |
| selector | <code>String</code> |  | Селектор элемента |
| source | <code>Object</code> \| <code>function</code> |  | Объект для сравнения стилей или функция-предикат |
| [message] | <code>String</code> | <code>CSS-свойства не изменились</code> | Сообщение об ошибке |

<a name="yaWaitForUrlChange"></a>

## yaWaitForUrlChange(prevUrl) ⇒ <code>Promise.&lt;Boolean&gt;</code>
Ждёт измнение урла страницы

**Kind**: global function  

| Param | Type | Description |
| --- | --- | --- |
| prevUrl | <code>String</code> | предыдущий url |

<a name="yaWaitForVisible"></a>

## yaWaitForVisible(selector, [timeout | message], [message]) ⇒ <code>Promise</code>
Обёртка над стандартной командой waitForVisible. Позволяет указывать произвольное сообщение об ошибке.

**Kind**: global function  

| Param | Type | Description |
| --- | --- | --- |
| selector | <code>String</code> | Селектор для элемента, появление которого нужно ждать |
| [timeout | message] | <code>Number</code> \| <code>String</code> | Таймаут в миллисекундах или Сообщение об ошибке |
| [message] | <code>String</code> | Сообщение об ошибке |

<a name="yaWaitImageLoaded"></a>

## yaWaitImageLoaded(selector, [timeout], [message]) ⇒ <code>Promise</code>
Проверяет, что картинка/фоновое изображение(любого блока) загрузилась.

**Kind**: global function  

| Param | Type | Description |
| --- | --- | --- |
| selector | <code>String</code> | Селектор для элемента, загрузку которого проверяем |
| [timeout] | <code>Number</code> | Таймаут в миллисекундах |
| [message] | <code>String</code> | Сообщение об ошибке |

<a name="Position"></a>

## Position : <code>&#x27;left-top&#x27;</code> \| <code>&#x27;right-top&#x27;</code> \| <code>&#x27;center-top&#x27;</code> \| <code>&#x27;left-bottom&#x27;</code> \| <code>&#x27;right-bottom&#x27;</code> \| <code>&#x27;center-bottom&#x27;</code> \| <code>&#x27;center-center&#x27;</code> \| <code>&#x27;left-center&#x27;</code> \| <code>&#x27;right-center&#x27;</code>
Функция клика по области элемента. Нужно для проверки того, что элемент кликабелен
не только в какой-то определенной области, а весь целиком

**Kind**: global typedef  

| Param | Type | Description |
| --- | --- | --- |
| _position | [<code>Position</code>](#Position) | место, в которое нужно кликнуть (н-р, 'left-top' - левый верхний угол) |
| _selector | <code>string</code> | селектор элемента |

<a name="yaWaitUntilMessageCallback"></a>

## yaWaitUntilMessageCallback ⇒ <code>string</code>
**Kind**: global typedef  
