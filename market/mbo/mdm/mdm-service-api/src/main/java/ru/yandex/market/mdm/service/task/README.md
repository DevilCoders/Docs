Временно создаем здесь package для работы с кастомным бизнес задачами для ДС

В дальнешем планируется увоз этого пакета в отдельный проект, поэтому рекомендуется руководствоваться следующими правилами разработки в нем:
* Запрещено обращаться к любым классам с другим пакетов, за исключением shared
* Все зависимости добавлять под раздел tasks в ya.make
