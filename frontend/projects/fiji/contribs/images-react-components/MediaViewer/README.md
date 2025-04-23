## Просмотрщик медиа-элементов

**DEPRECATED** Всё, что здесь написано, устраело и не отображает реальное положение дел. А оно такое - окно просмотра используется исключительно Картинками и только на десктопе. И в будущем планов расширять его на другие сервисы нет.

### На основе MediaViewer реализованы окна просмотров Картинок, Коллекций и публикаций в 1org.
1. [Картинки](https://yandex.ru/search/?lr=146&text=%D0%BA%D0%B0%D1%80%D1%82%D0%B8%D0%BD%D0%BA%D0%B8)
1. [Коллекции foreverdata](https://yandex.ru/search/?foreverdata=221489933&lr=146) *или* [Коллекции прод](https://yandex.ru/search/?text=%D0%BA%D0%B0%D0%BB%D0%B5%D0%BD%D0%B4%D0%B0%D1%80%D1%8C%202019&lr=146)
1. [1org десктоп](https://yandex.ru/search/?text=%D0%9B%D0%B8%D0%B3%D0%B0%20%D0%B4%D0%B6%D0%B5%D0%BD%D1%82%D0%B5%D0%BB%D1%8C%D0%BC%D0%B5%D0%BD%D0%BE%D0%B2%20%D0%90%D0%BB%D1%82%D0%B0%D0%B9%D1%81%D0%BA%D0%B8%D0%B9%20%D0%BA%D1%80%D0%B0%D0%B9&lr=54&noredirect=1)
1. [1org тачи](https://yandex.ru/search/touch/?text=%D0%9B%D0%B8%D0%B3%D0%B0%20%D0%B4%D0%B6%D0%B5%D0%BD%D1%82%D0%B5%D0%BB%D1%8C%D0%BC%D0%B5%D0%BD%D0%BE%D0%B2%20%D0%90%D0%BB%D1%82%D0%B0%D0%B9%D1%81%D0%BA%D0%B8%D0%B9%20%D0%BA%D1%80%D0%B0%D0%B9&lr=54&noredirect=1)

#### Код начинается здесь:
1. https://github.yandex-team.ru/serp/web4/blob/dev/src/experiments/imgwiz_react_viewer_enabled/features/Images/Images.components/ImageViewerApp/ImageViewerApp.tsx
1. https://github.yandex-team.ru/serp/web4/blob/dev/src/features/CollectionsViewer/Collections.components/CollectionsViewerApp/CollectionsViewerApp.tsx
1. https://github.yandex-team.ru/serp/web4/pull/25601/ + https://github.yandex-team.ru/serp/web4/pull/25864

### Storybook и стабы:
* https://turbo-docs.si.yandex-team.ru/story/dev/?path=/story/mediaviewer--simple
* https://github.yandex-team.ru/serp/turbo/blob/dev/platform/components/MediaViewer/__tests__/MediaViewerBase.tsx
* https://github.yandex-team.ru/serp/turbo/blob/dev/platform/components/MediaViewer/MediaViewer.stories.tsx
* https://yandex.ru/turbo?stub=mediaviewer%2Fbase.json

## Положение дел
Цель про единое окно https://goals.yandex-team.ru/filter?goal=57988
Окно просмотра активно втаскивается на сервис Картинки взамен старого окна просмотра на i-bem (https://goals.yandex-team.ru/filter?goal=53510).
Общий код нужно покрывать тестами (которых на MediaViewer мало + основная часть лежит в web4), а лишь затем рефакторить.

### Задачи и цели, про которые нужно знать
1. [IMAGESUI-10000](https://st.yandex-team.ru/IMAGESUI-10000): Desktop. Перетащить десктопный просмотрщик на React на сервис Картинки
1. [CMNT-629](https://st.yandex-team.ru/CMNT-629): [EPIC] Загрузка изображений и просмотр
1. [STARTREK-16187](https://st.yandex-team.ru/STARTREK-16187): Прототип Реактового просмотрщика
1. [SERP-84919](https://st.yandex-team.ru/SERP-84919): [web4] Оверлей каталога отеля
1. [Базовые фичи Мессенджера](https://goals.yandex-team.ru/filter?goal=55555)

## Подписывайтесь на задачу про рефакторинг
* [IMAGESUI-10113](https://st.yandex-team.ru/IMAGESUI-10113): Вынести основную сцену просмотрщика в отдельный компонент

## С чего начать
1. Дойти до @pskucherov и рассказать про планы.
1. Потключить компоненты из `@yandex-int/images-react-components` и `@yandex-turbo/core`
1. Попробовать заиспользовать окно просмотра, начав отсюда: https://github.yandex-team.ru/serp/turbo/blob/dev/platform/components/MediaViewer/__tests__/MediaViewerBase.tsx
1. По ходу дела задавать вопросы в чате https://q.yandex-team.ru/#/join/c3ee07bf-3e01-40a3-a47f-9d1c69825880
1. Публиковать правки по этой инструкции https://github.yandex-team.ru/serp/turbo/tree/dev/platform#как-выпустить-новую-версию-пакетов-компонентов
