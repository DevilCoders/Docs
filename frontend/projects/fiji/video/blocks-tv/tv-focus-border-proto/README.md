# tv-focus-border-proto

Блок прототипа стилистического оформления для анимированной рамки `tv-focus-border`. Определяет внешний вид рамки
для конкретного элемента интерфейса.

С помощью псевдоэлемента `:before` задаёт стиль и расположение рамки относительно сфокусированного элемента. К целевому
элементу миксуется вместе с модификатором темы. По умолчанию скрыт, отображается модификатором `visible`.

## Известные проблемы
1. Все размеры в стилях рамки должны быть заданы в rem или %, иначе будут большие погрешности при анимировании рамки;
1. Для круглых рамок `border-radius` должен быть ровно половину ширины (или меньше) иначе на SmartTV перестанет работать
скругление при анимации рамки;
1. Свойства `translateX` и `translateY` при анимации рамки учтены не будут.
