# Recorder 2.5

## Общая архитектура
Итак, как всем известно webvisor 2 загадочный и сложный компонент кода счётчика, по крайней мере он являлся таковым до недавнего времени. Давайте же в общем определимся как он работает.
<img src="architecture.jpg"
     alt="UML diagram"
     style="margin: 10px;" />
Данная упрощённая UML диаграмма показывает общее отношение к друг другу основных компонентов рекордера. Давайте определим ответственности каждого из таких компонентов чтобы лучше понять происходящее.

### Recorder
Контролирует инициализацию и деинициализацию всех подкомпонентов. Предоставляет другим компонентам доступ к метаинформации через утилиты внутри себя (например даёт доступ к замеру времени). Контролирует отправку уже записанных данных (в зависимости зависимый мы рекордер или нет).

### Indexer
Контролирует сбор информции о DOM элементах и распределяет её по времени чтобы избежать лагов. Подробнее в ридми касающегося индексера. Он НЕ занимается сбором информации о мутиациях, он всего лишь контролирует то что информация о конкретной ноде в конкретный момент времени собрана корректно.

### Наследники AbstractCaptor 
Их массив содержится внутри рекордера и их запуск и выключение контролируется им. Каждый кэптор занят сбором информации об одном или нескольких событиях лежащих в одном смысловом домене. Например TouchesCaptor собирает информацию о touchstart, touchend, и touchmove. Кэптор использует рекордер чтобы отправить эти эвенты дальше или получить доступ к метаинформации.

## Recorder
Функции которые выполняет рекордер:
- Инициализация всех субкомпонентов
- Определение является ли данный рекордер рабом или хозяином
- Контроль за отправкой данных
- Возможность создание рекордеров рабов напрямую

Теперь подробнее о немного неясных моментах. 
Если рекордер является рабом, он должен отсылать данные через message к своему хозяину в окне выше, если рекордер является хозяином, он должен слать данные через senderFunction которая передаётся ему в конструкторе. Сложность состоит в том, что в момент инициализации мы не можем понять является ли рекордер хозяином или рабом. Если в конструктор рекордера передан frameId, он является рабом, если рекордер запущен не в айфрейме, то это точно хозяин, но если рекордер запущен внутри айфрейма и ему явно не передан frameId, он может быть как рабом (если сверху есть другой рекордер), так и хозяином (если сверху нет другого рекордера). Определением статуса в таком случае занимается утилита iframeConnector которая занимается обменом сообщений между айфреймами (подробнее о её логике работы в readme в папке). До того как статус опредлеён данные должны накапливаться в буффере внутри рекордера.
