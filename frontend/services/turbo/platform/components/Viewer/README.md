## Просмотрщик

Просмотрщик — это модальное окно, открывающееся на весь экран. В просмотрщик можно
помещать содержимое разного типа, в первую очередь картинки.

Компонент вставляется в указанный DOM-узел через React-портал, поэтому он
отрисовывается только на клиенте. Таким образом, для использования компонента
просмотрщика, нужно подготовить для него заранее DOM-узел. Кроме того, просмотрщик
подкладывает под себя свою паранджу, обеспечивающую непросвечиваемость страницы под
просмотрщиком во время переворачивания устройства. DOM-узел под паранджу можно так
же создать отдельно, иначе просмотрщик создаст его сам.
