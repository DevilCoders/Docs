# Captors
Далее приведён список кэпторов с описанием того что они делают.

## AbstractCaptor
Родитель всех последующих кэпторов. Из интересного, хранит в себе логику подписки и отписки на события указанные в хэше handlers, в котором ключём является событие для подписки, а значением функция. Также содержит метод wrapInErrorLogger который стоит использовать.

## DeviceRotationCaptor
Ловит события поворота для мобильных устройств.

## FocusCaptor
Ловит события фокуса.

## IframeCaptor
Занимается записью событий из айфреймов лежащих в документе. Находит эти айфреймы по добавлению их в дерево и регистрации их через индексер. Занимается определением того нужно ли инъектировать внутрь таких айфреймов рабский рекордер проверяя их на about:blank или совпадение доменов. При вставки такого рекордера туда где он уже есть ничего страшного не случится, он просто свалится с ошибкой.
Также этот кэптор занят правкой таймстэмпов из айфреймов и выставлением им таймстэмпов относительно текущего айфрейма.

## InputCaptor
Ловит события ввода для элементов.
Занимается манки патчингом атрибутов value и checked для инпутов добавленных в DOM для записи програмно изменённых инпутов, предварительно проверив возможность такой подмены.
Занимается заменой на звёздочки значения инпутов, если данные инпуты содержат приватные данные, или если пользователь находится в евросоюзе (или проставляет флаг hidden для события).

## KeyStrokeCaptor
Ловит и отпрвляет нажатия особых клавиш и сочетаний клавиш для крипты.

## MouseCaptor
Ловит события мыши с троттлингом, и отправляет их на сервер.

## MutationCaptor
Обрабатывает мутации полученные из MutationObserver. Данные мутации бывают четырёх типов:
- Добавление элементов
- Удаление элементов
- Изменение атрибутов
- Изменение текста
Итак каждый из этих типов мутаций обрабатывается по-своему, но следуюет заметить, что перед их обработкой происходит сбор данных которые могут поменяться по мере обрабоки каждой последующей мутациией. Например при удалении мутации мы запоминаем какой парент у них был до момента их удаления (потому что одна и та же нода может быть в этой же пачке мутаций и вставлена). Также мы отдельно собираем информацию обо всех изменённых атрибутах для каждой ноды, чтобы отправить события скопом.

## PageCaptor
Собирает изначальный код страницы пользуясь той же логикой что и MutationCaptor для добавления нод, только проще.

## ResizeCaptor
Записывает ресайзы экрана. В рабских айфреймах он тоже работает, но игнорируется плеером (а ресайз самих айфреймов отрисоввывается из-за изменения их аттрибутов).

## ScrollCaptor
Записывает скроллы как элементов так и документа.

## SelectionCaptor
Записывает выделение контента при помощи мышки.

## SrcsetLoadCaptor
Это нужно для того чтобы определять загрузку изображений для которых указаны srcset. Поскольку загрузка таких элементов не вызывает мутаций а srcset не работает при воспроизведении в айфрейме (по какой-то причине) пришлось делать такой костыль.

## TouchesCaptor
Записывает все события из группы тачей.

## WindowFocusCaptor
Записывает события фокуса и блюра для окна. Данные события нужны API чтобы определять когда при нескольких открытых вкладках происходит переключение с одной на другую.

## ZoomCaptor
Записывает зум при помощи древней магии которая работает в ряде старых мобильных браузеров и больше нигде. Ждём нормального апи для событий зума (хром вроде хотел добавить).