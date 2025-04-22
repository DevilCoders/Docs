Дерево чекбоксов со связанным поведением при изменении состояний

Стандартное поведение при изменении моды "checked" чекбокса:
 - все его потомки выставляют такое же значение этой моды
 - его родитель выставляет моду "checked" равную "yes" если такое состояние У ВСЕХ его потомков,
   иначе он убирает эту моду

Использование:

    {
        block: 'b-checkbox-tree',
        items: [
           {
               checkboxAttrs: { value: 'val_2',  name: 'text', tabindex: 2 }
               label: iget('Стационарные компьютеры, ноутбуки, другие устройства')
           },
           {
               checkboxAttrs: { value: 'val_2',  name: 'text', tabindex: 2 }
               label: iget('Смартфоны'),
               subs: [
                   { value: 'iphone', label: iget('iPhone') },
                   { value: 'android_phone', label: iget('Смартфоны Android') }
               ]
           },
           {
               checkboxAttrs: { value: 'val_2',  name: 'text', tabindex: 2 }
               label: iget('Планшеты'),
               subs: [
                   { value: 'ipad', label: iget('iPad') },
                   { value: 'android_tablet', label: iget('Планшеты Android') }
               ]
           }
       ]
    }


Где items - данные для построения дерева.

Каждый item может содержать поля:
 - checkboxAttrs - объект, содержащий аттрибуты для нативного чекбокса (аналогично блоку checkbox)
 - label - строка, метка чекбокса (отрисоввается справа)
 - subs - массив элементов item, работают как потомки

