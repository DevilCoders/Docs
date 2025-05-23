## Сетка

Для раскладки имеются следующие сущности:
1. Блок `container` — контейнер, внутри которого может лежать произвольный блок. У контейнера могут быть модификаторы:
    * `_center` — спозиционировать контейнер по центру, у такого контейнера заданы ограничения по ширине `980-1340px`.
    * `_main` — растягивается по всей доступной высоте, чтобы прижать после себя контейнер с футером к низу страницы.
2. Блок `row` – строка для организации колонок, не имеет визуальных стилей, выстраивает содержимое по горизонтали.
3. Элемент `row__col` — колонка с боковыми отступами 20px, у которой должен быть задан размер, например: `_size_4`.

Модификатор `_size_N` указывает ширину элемента, где `N` — это количество столбцов сетки от 1 до 24. Ширина указывается в процентах и рассчитывается по формуле `N * 100 / 24`.

Стандартные отступы раскладки нужно воспринимать, как стандартные стили элементов в браузере. Если нужно, вебмастер может их легко переопределить в кастомном CSS для своей страницы.
