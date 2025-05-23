# Борьба с фродерами aka "пошаговое наказание"

## Продуктовая часть

### Проблема:
* мы холдим с пользователя депозит
* даем ему начать поездку
* он выкатывает самокат на SUM > deposit
* на него вешается долг в размере SUM - deposit

Получается, что сейчас потенциальный фродер может безлимитно кататься всего за 500 рублей

### Решение:
Чтобы это полечить, предлагается совершать какие-то действия в случае, если мы не смогли списать деньги за сессию по вине пользователя, например: 
* мы холдим депозит и пускаем пользователя в поездку
* когда он выкатывает депозит и одну дискретизацию, пытаемся списать с него деньги
* если не получилось по его вине, то совершаем какое-нибудь действие (ограничение скорости / выключение газа)

Ожидаем, что при таких действиях количество "бесконечных" сессий снизится (сейчас поездки на 1000+ рублей в Краснодаре составляют примерно треть от общего количества, из них большинство не оплачено)

## Техническая часть:

### Сейчас логика вокруг замедлений/выключений газа размазана по следующим местам: 
* боты Драйва (есть объяснение механики тут: [wiki](https://wiki.yandex-team.ru/users/sapunovnik/boty-tegi-i-vsja-xurma))
* телематика (есть костыль, который в heartbeat'е смотрит на заряд, и в зависимости от него устанавливает ограничения: [code](https://a.yandex-team.ru/arc/trunk/arcadia/scooter/telematics/server/library/connection.cpp?rev=r9406237#L983))
* периодик в scooters-misc ([тикет](https://st.yandex-team.ru/SCOOTERDEV-244))
* **вопрос к ревьюверам:** я ничего не упустил?

### Предложение 0 (самое простое, проблемное): 
* Есть stq-таски ``scooters-session-watcher``: можно в них добавить отслеживание платежей, и при выполнении каких-нибудь условий вешать какие-нибудь теги
  
У этого решения есть проблема: сейчас с тегами замедления и так происходят непонятные вещи, и нет единой точки синхронизации. С добавлением +1 источника тегов ситуация только ухудшится

### Предложение 1 (достаточно большое по реализации), состоит из 3 частей:
#### **Часть 1**
* Добавить обработчик, который будет принимать события и включать/выключать ограничения скорости / газ (на основе событий + своих внутренних знаний о самокате/сессии). Этот обработчик — единственное место, в котором устанавливаются ограничения. У него будет информация о текущем установленном ограничении и его причине, локации и заряде самоката.

#### **Часть 2**
* В stq-таске ``scooters-session-watcher`` добавить отслеживание платежей, и при неудаче формировать событие и отправлять его в обработчик (ручка ``/billing/payment/info`` по ``session_id`` может показывать платежи)

#### **Часть 3**
* Добавить периодик (похожий на [этот](https://st.yandex-team.ru/SCOOTERDEV-244)), который будет следить за скоростными ограничениями / газом / чем-нибудь еще на всем флоте, упрощенно работает так: 
    * просыпается раз в X cекунд
    * смотрит на локации, заряд, текущий стейт самокатов
    * на основе данных из предыдущего пункта формирует событие, отправляет его в обработчик

Этот периодик не относится напрямую к антифроду, но без него с замедлениями будет еще больший хаос, чем сейчас

#### **Notes:**
* я намеренно разделяю 2 и 3 части, т к у них разная природа и частота проверки (ок проверять платежи раз в минуту, не ок проверять локацию раз в минуту)
* события могут передаваться различными способами: по http, через логброкер, через базу. я не вижу проблем у самого простого решения в виде "вызвать функцию ``ProcessEvent`` у класса ``ScooterEventsManager``", поэтому в первой итерации предлагаю использовать его

Это конечная картина, к которой хотим прийти, чтобы asap полечить фрод, см предложение 2.

### Предложение 2 (упрощенное п. 1, выключаем фродерам газ):
* часть 2 остается без изменений
* части 1 и 3 упрощаются до работы только с включением / выключением газа (т к с замедлениями больше внешних процессов)


#### **Таймлайн:**
* 2 часть (1-2d)
* 1 часть (газ) (2-3d)
* 3 часть (газ) (1-2d)
* включение + раскатка + фикс возможных багов (2d)
* <тут уже есть пользя для антифрода>
* 1 часть (замедления) (1d)
* 3 часть (замедления) (1d)
* включение + раскатка + фикс возможных багов (5d)
