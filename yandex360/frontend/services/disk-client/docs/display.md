# Отображение листинга и ресурса

Модель состояния контекста хранит несколько параметров, которые влияют на внешний вид листинга и ресурса:

* `groupBy`
* `display`

Первый принимает значения `month` или `none`, а второй — `normal` или `photostream`.

Первый параметр отвечает за то как будут сгруппированы ресурсы в листинге, например, в фотокамеры они сгруппированы по дате, соотвественно, `groupBy` принимает значение `month` — сейчас, по сути, это влияет на внешний вид листинга: наличие или отстутсвия визуальных групп.

Второй парамерт меняет внешний вид ресурса: «как в фотокамере» и «обычный».

Кобминируя эти значения можно получить 4 типа листинга.

## Обычный листинг

Обычный листинг (`groupBy: none`, `display: normal`) не содержит групп, ресурсы содержат имена и нормальные оступы.

![](http://jing.yandex-team.ru/files/vitkarpov/2014-05-22_1615.png)

## Листинг фотокамеры

Листинг в фотокамере (`groupBy: month`, `display: photostream`) — это большие фреймовые превью и группы.

![](http://jing.yandex-team.ru/files/vitkarpov/2014-05-22_1605.png)

## Листинг в соц.сетях

Листинг в соц.сетях (`groupBy: none`, `display: photostream`): большие фреймовые превью, но без групп — все ресурсы идут друг за другом в строках

![](http://jing.yandex-team.ru/files/vitkarpov/2014-05-22_1609.png)

## Неиспользуемые тип листинга

Можно составить еще одну комбинацию, которая сейчас на проекте не используются: `groupBy: month` и `display: normal`

![](http://jing.yandex-team.ru/files/vitkarpov/2014-05-22_1612.png)

Группы как в фотокамере, но ресурсы как в обычном листинге: с именами и большими отступами.
