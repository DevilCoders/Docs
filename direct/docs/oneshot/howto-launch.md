[Написание кода ваншота](howto-code.md) <br/>
[Тестирование ваншота](howto-testing.md) <br/>
[Доставка ваншота в продакшен](howto-release.md) <br/>

# Как запустить ваншот

Запускать ваншоты может пользователь Директа с правами суперпользователя или разработчика. Безопасные ваншоты можно запускать без апрува, а для обычных ваншотов потребуется подтверждение от одного из апруверов. Список апруверов указывается в аннотации `@Approvers`, подробнее читать [здесь](howto-code.md#approvers)

Общий флоу запуска:

- суперпользователь или разработчик (роль) создает запуск;
- для обычных ваншотов (кроме безопасных) один из апруверов подтверждает запуск (ваншот в этот момент не начинает выполняться!).
- создатель запуска в удобное для него время инициирует выполнение ваншота.

## Создаем запуск

Как создать запуск ваншота:

- заходим на страницу ваншотов ([прод](https://direct.yandex.ru/internal_tools/#oneshots) | [ТС](https://test-direct.yandex.ru/internal_tools/#oneshots)) в InternalTools и видим свой ваншот в списке — у него есть ссылки на тикет и на исходный код; в тикете будут отражаться события, связанные с этим ваншотом;
- выбираем ваншот в селекте;
- проверяем, требует ли ваншот входные данные и в каком формате: переходим по ссылке "Открыть в Arcanum..." из таблички с ваншотами и смотрим на тип первого параметра метода `execute` (если тип — `Void`, то ваншот не принимает входные данные).
- если ваншот требует входные данные, то вставляем их в соответствующее поле в формате json
- нажимаем кнопку "Запросить апрув".
- отлично! теперь на странице запусков ([прод](https://direct.yandex.ru/internal_tools/#oneshot_launches) | [ТС](https://test-direct.yandex.ru/internal_tools/#oneshot_launches)) можно увидеть запуск ваншота (но ваншотилка еще не начала выполнять его).

Сперва ваншотилка выполнит метод ваншота `validate`, передав ему на вход сериализованный объект входных данных, которые вы указали в поле ввода. Статус валидации отображается в веб-интерфейсе на странице запусков ([прод](https://direct.yandex.ru/internal_tools/#oneshot_launches) | [ТС](https://test-direct.yandex.ru/internal_tools/#oneshot_launches)). Обычно метод валидации вызывается в течение нескольких секунд после создания запуска. Если спустя 5 минут валидация не выполнена, значит что-то пошло не так.

Если валидация провалена, то статус будет равен `INVALID`. В этом случае вы можете перейти в логи по ссылке "Открыть в logviewer" и посмотреть список ошибок валидации.

Если валидация прошла успешно, то статус валидации будет равен `VALID`. В этом случае для запуска необходимо получить апрув от одного из апруверов (для безопасных ваншотов не требуется).

## Получаем подтверждение

Зовем апрувера и просим его подтвердить запуск, сообщив ему id запуска, чтобы он не перепутал запуски одного и того же ваншота разными людьми.

{% note warning %}

Будьте внимательны: не путайте id запуска и id ваншота. У каждого ваншота может быть много запусков, и даже в один момент времени несколько запусков от разных людей могут ожидать апрува.

{% endnote %}

## Для апрувера: подтверждаем запуск ваншота

{% note info %}

После подтверждения запуска ваншот не запустится сам по себе. Создатель запуска сможет самостоятельно запустить его в нужный момент.

{% endnote %}

{% note warning %}

Будьте внимательны: не путайте id запуска и id ваншота. У каждого ваншота может быть много запусков, и даже в один момент времени несколько запусков от разных людей могут ожидать апрува.

{% endnote %}

Пошаговая инструкция для апрувера:

- заходим на страницу запусков ([прод](https://direct.yandex.ru/internal_tools/#oneshot_launches) | [ТС](https://test-direct.yandex.ru/internal_tools/#oneshot_launches));
- ищем запуск по id запуска;
- внимательно проверяем, можно ли запускать ваншот с этими входными данными (в тот момент, когда автор запуска планирует инициировать его выполнение);
- **если все в порядке**, выбираем в селекте ваншот по имени **и по id запуска** — на каждый класс ваншота может быть зарегистрировано несколько запусков с разными параметрами;
- выбираем в селекте "Действие" опцию "Подтвердить";
- нажимаем кнопку "Выполнить";
- готово! теперь запуск ваншота подтвержден и тот, кто запросил этот запуск, сможет инициировать непосредственно выполнение ваншота в любое удобное для него время.

## Инициируем выполнение

У нас есть подтвержденный запуск ваншота, теперь в любой удобный момент времени можно начать непосредственно выполнение:

- заходим на страницу запусков ([прод](https://direct.yandex.ru/internal_tools/#oneshot_launches) | [ТС](https://test-direct.yandex.ru/internal_tools/#oneshot_launches));
- выбираем в селекте ваншот по имени **и по id запуска** — на каждый класс ваншота может быть зарегистрировано несколько запусков с разными параметрами;
- выбираем в селекте "Действие" опцию "Запустить";
- нажимаем кнопку "Выполнить";
- готово! теперь на странице потоков выполнения ([прод](https://direct.yandex.ru/internal_tools/#oneshot_launch_data) | [ТС](https://test-direct.yandex.ru/internal_tools/#oneshot_launch_data)) можно отслеживать состояние.
