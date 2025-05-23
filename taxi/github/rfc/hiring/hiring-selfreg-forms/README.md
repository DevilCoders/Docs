#### Название сервиса
hiring-selfreg-forms

#### Задачи сервиса
##### Какую продуктовую проблему решает сервис?
Автоматизирование создания лидов с формы саморегистрации с проверкой телефона, сохранением анкеты на каждом шаге. 
На старте -- для саморгистрации курьеров Еды. 

##### Почему нельзя решить эту задачу без разработки нового сервиса существующими решениями?
В существующих системах такой функциональности нет

##### Как именно сервис будет решать поставленные перед ним задачи?
- Принимать данные
- Валидировать данные
- Проверять телефон по одноразовому коду
- Проверять на залогиненность в Еде
- Сохраняет введенные данные на каждой странице анкеты
- Получать доступные вакансии в городе
- Класть в очередь stq, которая создаст тикеты

##### Разрабатывается один сервис или система?
- [x] Один
- [ ] Система

#### Взаимодействие
##### Сервис внутренний или внешний?
- [x] Внутренний
- [ ] Внешний

##### С кем взаимодействует сервис?
- hiring-authoproxy
- hiring-rate-accounting
- experiments3
- personal
- configs
- infranaim-api
- Api Еды

##### Использование Passenger Authorizer
https://wiki.yandex-team.ru/taxi/backend/architecture/passenger-authorizer/
- [ ] Да

##### Использование Driver-authorizer
https://wiki.yandex-team.ru/taxi/backend/architecture/driver-authorizer/
- [ ] Да

##### Залогиненность
Залогиненность означает возможность запуска сервиса в доменах yandex.ru|yandex-team.ru, возможность залогинить пользователя, возможность проверить или выставить cookie
- [ ] Да
	
##### Использование Blackbox
https://doc.yandex-team.ru/blackbox/concepts/about.xml
- [ ] Да

##### Использование MDS
https://wiki.yandex-team.ru/mds/s3-api/
- [ ] Да

##### Какие базы использует?
- [x] PostgreSQL
- [ ] Mongo
- [ ] Redis
- [ ] Other

##### Какие периодические процессы?
- Очередь stq: отправка в infranaim-api.

#### Хранение и обработка данных
##### Планируется обработка персональных данных
Удостоверения личности, данные банковских карт, финансовая информация, ФИО + номер телефона, персональные прогнозы (как у Крипты) и т.д. 
- [x] Да

##### Какие данные и по какой схеме сервис будет хранить в базе?
- На входе все ПД будут обменяны на pd_id.
- Данные анкеты

##### Какой объем данных будет храниться и какой объем будет изменяться в единицу времени?
- До 1МБ/секунду
- До 1 ГБ хранения

##### Какие операции над данными заложены?
- Валидация
- Хранение 

##### Есть ли какой-то стейт в памяти, как он обновляется и валидируется?
Нет

#### Отказоустойчивость и масштабируемость
##### Какая нагрузка ожидается?
Меньше 20 RPS

##### Какие фолбеки предусмотрены на сам этот сервис?
Никаких

##### Какие фолбеки предусмотрены внутри этого сервиса на взаимодействие с другими сервисами?
- hiring-authoproxy. Если недоступен hiring-authoproxy, то заявка не прилетит в hiring-selfreg-forms
- Дефолтное значение вакансии при условии, что не удалось получить вакансии из E3 и hiring-rate-accounting 
- infranaim-api. Если сервис не ответил, то stq пытается переотправить. На графиках будет виден рост очереди.
- personal. Без него сервис не работает 

##### Какие возможности масштабируемости закладываются?
Поддержка форм саморегистрации не только для Еды

##### Какие точки отказа есть в сервисе?
- hiring-authoproxy
- infranaim-api
- personal

#### Метрики
##### Укажите ключевые продуктовые метрики сервиса, за которыми планируете следить
- Количество заявок

##### Укажите технические метрики
- Среднее время обработки заявки
- RPS
- очереди stq 

#### Планы роста
##### Какая функциональность ожидается в сервисе в будущем?
Поддержка форм саморегистрации не только для Еды

##### Какое изменение нагрузки планируется?
Нагрузка будет расти, но вряд ли драматически. Менее 100 RPS

##### Активно ли будет изменяться сервис?
- [x] Да

#### Общая информация
##### Менеджер
@ikolbey

##### Релиз (предполагаемая дата)
13.05.2020

##### Язык, на котором пишется сервис
- [ ] C++
- [x] Python3
- [ ] Other

##### Ссылка на тикет, в рамках которого идет разработка
[INFRANAIM-4755](https://st.yandex-team.ru/INFRANAIM-4755)

##### Дополнительные согласования
Нет

##### Комментарий
Нет
