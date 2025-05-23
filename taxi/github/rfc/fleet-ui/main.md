### Архитектурное описание сервиса - fleet-ui

### Название сервиса
fleet-ui

### Какую продуктовую проблему решает сервис?
Индивидуальная настройка пользовательского интерфейса Оптеума.
Настройка отображения пунктов меню Оптеума в зависимости от параметров парка и прав пользователя.
Возможность быстрого изменения конфигурации пунктов меню Оптеума через админку или конфиг без перевыкатки сервисов.
В будущем - хранение персональных настроек интерфейса пользователя.

### Почему нельзя решить эту задачу без разработки нового сервиса существующими решениями?
На данный момент не существует сериса,
который отвечал бы за логику построения пользовательского интерфейса Оптеума,
а также хранил бы персональные настройки пользователей.

### Как именно сервис будет решать поставленные перед ним задачи?
Сервис будет принимать user_ticket и park_id.
По user-ticket будут определены права пользователя.
По park_id - параметры парка.
Также в будущем сервис будет хранить у себя настройки интерфейса пользователя.
Сейчас они хранятся в local storage.
Это ненадежно и создает сложности при работе с мобильными устройствами.
Перенос настроек в сервис позволит собирать статистику в целях улучшения UX.

### Разрабатывается один сервис или система?
Один сервис

### С кем взаимодействует сервис?
- Оптеум: для возвращения пунктов меню для отображения
- fleet-parks для получения информации о парке
- dispatcher-access-control для получения информации о пользователе и его правах и доступах
- в будущем админка (tariff editor) для создания и настройки пунктов меню

### Какие базы использует?
На момент запуска - нет.
В дальнейшем - своя база для хранения личных настроек пользователя

### Какие периодические процессы?
Нет

### Планируется обработка персональных данных
Нет

### Какие данные и по какой схеме сервис будет хранить в базе?
- park_id
- user_id
- параметр
- значение
- дата установки

### Какой объем данных будет храниться и какой объем будет изменяться в единицу времени?
Среднее количество сотрудников в парке 10
Количество парков 100к (до 200к)
Количество строк в базе 1М
При среднем размере строки в 20-30б получаем 20-30 (40-60) мегабайт.

### Какие операции над данными заложены?
- Чтение данных
- Изменение существующих настроек пользователей
- Добавление новых настроек пользователей

### Есть ли какой-то стейт в памяти, как он обновляется и валидируется?
Нет

### Какая нагрузка ожидается?
50-100rps

### Какие фолбеки предусмотрены на сам этот сервис?
Фолбеки на сервис не планируются.

### Какие фолбеки предусмотрены внутри этого сервиса на взаимодействие с другими сервисами?
Возможно, получать дефолтные значения при отказе сервисов fleet-parks или dispatcher-access-control.

### Какие возможности масштабируемости закладываются?
Горизонтальное масштабирование

### Какие точки отказа есть в сервисе?
- Конфиги
- БД

### Укажите ключевые продуктовые метрики сервиса, за которыми планируете следить
Скорость работы SPA
Скорость добавления новых возможностей в диспетчерскую

### Укажите технические метрики
Дефолтные дашборды

### Какая функциональность ожидается в сервисе в будущем?
Хранение персональных настроек интерфейса пользователя
Расширение логики построения интерфейса (заголовок с брендированием, доступные языки и т.д)

### Какое изменение нагрузки планируется?
Пропорционально количеству парков и пользователей

### Активно ли будет изменяться сервис?
Да
