Форматы модалок

1. createRootModal. Позволяет удобно работать с данными из redux. При открытии модалки берет самые актуальные данные из redux, а при применении сообщает об изменении только измененных данных.

2. createModal. Позволяет модифицировать состояние, которое не хранится в redux. Обычно это дочерние модалки.

3. createDataModal. Позволяет создавать модалки для отображения данных. Можно подсоединить напрямую к redux или передавать данные через метод открытия модалки

4. createActionModal. Позволяет создавать модалки для выбора конкретного действия.
