# Методы API

В окне, где запущен редактор (webView) доступен глобальный объект `EDITOR_API`,
содержащий методы:

  — `getData()` — возвращает сериализованную модель данных редактора [code](https://github.yandex-team.ru/UFO/notes-editor/blob/master/src/api/getData.js);

  — `getHeader()` — возвращает заголовок, когда он реализован в редакторе [code](https://github.yandex-team.ru/UFO/notes-editor/blob/master/src/ckeditor5-note-header/src/index.js);


  — `getSnippet()` — возвращает снипет редактора, это первая непустая строка в случае если у нас есть непустой заголовок или вторая, если заголовок есть и пуст [code](https://github.yandex-team.ru/UFO/notes-editor/blob/master/src/api/getSnippet.js);

  — `getImageList()` — возвращает список url всех использованных в инструменте картинок [code](https://github.yandex-team.ru/UFO/notes-editor/blob/master/src/api/getImageList.js);

  — `getFullState()` — возвращает полную сериализованную модель данных редактора (header, snippet, data, imageList) [code](https://github.yandex-team.ru/UFO/notes-editor/blob/master/src/api/getFullState.js);

  — `invokeAndSend(requestId, methodName, parametersJsonList)` — Вызывает метод methodName у объекта EDITOR_API c параметрами и parametersJsonList передает результат через вызов `HOST_API.processInvocationResult(requestId, result)` [code](https://github.yandex-team.ru/UFO/notes-editor/blob/master/src/api/invokeAndSend.js);

  — `setData(data)` — применяет переданные данные [code](https://github.yandex-team.ru/UFO/notes-editor/blob/master/src/api/setData.js);

  — `getDeltas(from, to)` — Получаем список дельт из истории документа [code](https://github.yandex-team.ru/UFO/notes-editor/blob/master/src/api/getDeltas.js);

  — `setDeltas(stringifiedDeltas)` — Устанавливает документу историю из deltas в виде JSON строки [code](https://github.yandex-team.ru/UFO/notes-editor/blob/master/src/api/setDeltas.js);

  — `getVersion()` — Получение текущей версии документа в виде числа [code](https://github.yandex-team.ru/UFO/notes-editor/blob/master/src/api/getVersion.js);

  — `speechKit`

  - `beginSpeaking()` - Старт диктовки. После этого вызова (до вызова endSpeaking()) пользователь не должен иметь возможности изменить содержимое редактора стандартным способом - только через setSpeechData. Имеется возможность вызова beginSpeaking без вызова endSpeaking, если хотим сообщить, что текущая фраза закончилась, но диктовка ещё продолжается. [code](https://github.yandex-team.ru/UFO/notes-editor/blob/master/src/api/speechKit.js);

  - `setSpeechData()` - Передача данных диктовки. Новая порция данных заменяет предыдущую, если они обе переданы после beginSpeaking. [code](https://github.yandex-team.ru/UFO/notes-editor/blob/master/src/api/speechKit.js);

  - `endSpeaking()` - Конец сессии диктовки. [code](https://github.yandex-team.ru/UFO/notes-editor/blob/master/src/api/speechKit.js);

  — `listen(stringifiedEventNames)` — Подписка на события, получает на вход список событий (в формате JSON-массива ["event_name_1", ..., "event_name_n"]) при срабытывании которых вызывается метод `HOST_API.fire('event_name', {…})` [code](https://github.yandex-team.ru/UFO/notes-editor/blob/master/src/api/listen.js) Поддерживаемые события: commandsChanged, scroll;

  — `removeListen(stringifiedEventNames)` — Отписка от событий, получает на вход список событий (в формате JSON-массива ["event_name_1", ..., "event_name_n"]) [code](https://github.yandex-team.ru/UFO/notes-editor/blob/master/src/api/removeListen.js) Поддерживаемые события: commandsChanged, scroll;

  — `getCommandsState()` — Получение объекта с информацией об активных коммандах в виде `{ command_name_1: true, command_name_2: false, command_name_3: true, ... command_name_n: false}`. Для команд, которые могут быть неактивны для нажатия (undo/redo), передается значение isEnabled. Для остальных команд передается информация включены ли они на данном элементе, в windows - это checked,
  в ckeditor – value [code](https://github.yandex-team.ru/UFO/notes-editor/blob/master/src/api/getCommandsState.js);

  — `getScroll()` — Получение JSON представления объекта с положением скрола вида `{ top:<положение скрола от верха>, left:<положение скрола от левого края> }` [code](https://github.yandex-team.ru/UFO/notes-editor/blob/master/src/api/getScroll.js);

  — `bold()` — делает выделенный фрагмент текста жирным;

  — `italic()` — делает выделенный фрагмент текста курсивом;

  — `underline()` — делает выделенный фрагмент текста подчёркнутым;

  — `strikethrough()` — делает выделенный фрагмент текста зачёркнутым;

  — `checkbox()` — делает выделенный фрагмент параграфом с чекбоксом;

  — `bulletedList()`;

  — `numberedList()`;

  — `heading1()`;

  — `heading2()`;

  — `alignmentLeft()` — выравнивает параграфы и заголовки по левому краю;

  — `alignmentCenter()` — выравнивает параграфы и заголовки по центру;

  — `alignmentRight()` — выравнивает параграфы и заголовки по правому краю;

  — `blockQuote()` — делает выделенный фрагмент текста цитатой;

  — `Image`

  - `image(JSON({ url: <image_url>, x: <Number>, y: <Number> })` — вставляет картинку в позицию курсора, либо если переданы координаты то в позицию X, Y(предварительно разбивает блок аналогично нажатию `Enter`) [code](https://github.yandex-team.ru/UFO/notes-editor/blob/master/src/ckeditor5-image/src/imagecommand.js);

  - `refreshImage(JSON({ url: <image_url> })` — Обновить каритнку, чтобы она стала показываться вместо placeholder'a [code](https://github.yandex-team.ru/UFO/notes-editor/blob/master/src/api/refreshImage.js);

  - `onUploadProgress(JSON({ id: number, total: number, uploaded: number })` — Обновить прогресс сохранения файла. Входные данные - объект с числовым полем id загружаемой картинки и полями total и uploaded (числовые в байтах).  [code](https://github.yandex-team.ru/UFO/notes-editor/blob/master/src/api/refreshImage.js);

  - `onUploadComplete(JSON({ id: number, url: string })` — Сообщить об успешном сохранении файла. Входные данные - объект с числовым полем id загружаемой картинки и текстовым полем url с новым адресом картинки.  [code](https://github.yandex-team.ru/UFO/notes-editor/blob/master/src/api/refreshImage.js);

  - `onUploadFailed(JSON({ iid: number, url: reason })` — Сообщить об ошибки при сохранении файла. Входные данные - объект с числовым полем id загружаемой картинки и текстовым полем reason с причиной ошибки.  [code](https://github.yandex-team.ru/UFO/notes-editor/blob/master/src/api/refreshImage.js);

  — `undo()`;

  — `redo()`;

  — `reinitialize()` - вызывает переинициализацию редактора, метод выполняется асинхронно, так что надо ожидать вызова `HOST_API.ready`;

  — `focus()` - ставит курсор в конец поля редактирования текста;

  — `focusHeader()` - ставит курсор в конец поля редактирования заголовка;

В окне, где запущен редактор (webView) также должен быть доступен глобальный объект `HOST_API`, реализованный средой исполнения и
содержащий методы:

  — `fire(eventName, eventValue)` - метод будет вызваться при срабатывании события именем eventName (строка) и в него будет передаваться объект события (json-строка);

  — `ready()` - метод вызывается при инициализации редактора.

  — `platform()` - метод возвращает строку с названием платформы. Например `"windows"` или `"android"`

  — `upload(fileMetaDataJson, fileDataArray)` - метод загрузки файла с объектом метаданных и данными файла. Файл может быть передан либо как URL, либо как ByteArray

объект метаданных - это JSON строка, которая парсится в обект с полями
- id - номер запроса на загрузку, number
- lastModified - дата изменения, number в миллисекундах от 01.01.1970
- size - размер в байтах, number
- name - имя, string
- type - строка вроде image/jpeg, string
- src - адрес картинки в интеренете, если указывается, то fileDataArray не передается, string

данные файла - это массив типа ArrayBuffer (не сериализованный)

  — `abortUpload(fileMetaDataJson)` - метод отменяет загрузку файла Объект метаданных содержит единственное поле - id

  — `openImage(fileMetaDataJson)` - метод открывает изображение в нативном приложении. Объект метаданных содержит единственное поле - url

  — `imageMenu(fileMetaDataJson)` - метод открывает изображение в нативном приложении. Объект метаданных содержит единственное поле - url
