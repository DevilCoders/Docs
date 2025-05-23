# Вставить таблицу

## Как вставить простую таблицу {#simple-table}

[Простые таблицы](static-markup/grids.md) — это статические таблицы, которые оформляются вручную с помощью разметки {{ wiki-name }} или Markdown.

Чтобы разместить таблицу в тексте, используйте разметку:

```
| Заголовок 1 | Заголовок 2 | Заголовок 3 |
| --- | --- | --- |
| ячейка 11 | ячейка 12 | ячейка 13 |
| ячейка 21 | ячейка 22 | ячейка 23 |
```

{% cut "Как выглядит результат" %}

![](../_assets/wiki/table-with-border.png)

{% endcut %}

## Как вставить динамическую таблицу {#grid}

[Динамическая таблица](pages-types.md#grid) — таблица с возможностью задать тип данных столбца, отсортировать значения или сделать ячейку обязательной для заполнения. Вы можете использовать таблицу напрямую или [встроить ее в вики-страницу](#section-integrate-table).

{% if audience == "draft" %}
Такую таблицу можно редактировать прямо на вики-странице (если при копировании кода таблицы не выбрана опция **Только для чтения**). Все изменения будут автоматически применяться к основной таблице и всем ее вхождениям в другие страницы.
{% endif %}

### Как создать и разместить таблицу на вики-странице {#section-add-table-button}

Чтобы создать таблицу и разместить ее в тексте вики-страницы:

1. На панели в верхней части вики-страницы нажмите значок ![](../_assets/wiki/add-dynamic-grid.png). В тексте появится [код таблицы](actions/grid-reference.md): 
    
    ```
    {{grid page="{{ wiki-pagename }}/grid-2021-01-24t163048" width="100%"}}
    ```

    Созданная таблица станет подразделом текущей страницы.

1. Нажмите **Сохранить**.

1. [Заполните таблицу](edit-grid.md).

### Как встроить существующую таблицу {#section-integrate-table}

Чтобы встроить динамическую таблицу в вики-страницу:

1. Откройте таблицу и нажмите кнопку **Редактировать**.

1. На панели слева нажмите значок **</>**.

1. Настройте параметры для вставки таблицы.

1. Скопируйте код таблицы и вставьте в текст вики-страницы.

### Как фильтровать строки и столбцы таблицы {#filter}

Вы можете вставить динамическую таблицу на вики-страницу так, чтобы отображались только заданные столбцы или строки таблицы, которые соответствуют определенным условиям. Для этого:

1. Получите код для вставки таблицы и разместите его в тексте вики-страницы.

1. Чтобы выбрать столбцы таблицы, которые будут отображаться на странице, добавьте к коду таблицы параметр `columns`. Подробнее об использовании этого параметра читайте в разделе [{#T}](actions/grid-reference.md#col-filter).

1. Чтобы задать условия для отображения строк таблицы в зависимости от значений в заданных ячейках, добавьте к коду таблицы параметр `filter`. Подробнее об использовании этого параметра читайте в разделе [{#T}](actions/grid-reference.md#row-filter).

### Как перейти к источнику встроенной таблицы {#go-to-source}

Чтобы открыть оригинал таблицы, встроенной в вики-страницу:

1. Внизу таблицы нажмите значок ![](../_assets/wiki/table-settings-footer.png).

1. Выберите **Родительская таблица**.

#### См. также

- [{#T}](edit-grid.md)

- [{#T}](import-page.md)

- [{#T}](static-markup/csv.md)