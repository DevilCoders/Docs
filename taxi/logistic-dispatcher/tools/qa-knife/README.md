# qa-knife

Утилита командной строки, которая позволяет одной командой создавать различные заказы в cargo: без отправления curl-ов, генерации tvm-тикетов.

## Установка

Чекаутим каркас arcadia и переходим в него:

```
svn cat svn+ssh://arcadia.yandex.ru/arc/trunk/arcadia/ya | python - clone
cd arcadia
```

### Через сборку аркадийного таргета (ubuntu)

Чекаутим все необходимое для инструмента и собираем его:

```
ya make --checkout taxi/logistic-dispatcher/tools/qa-knife
```

### Через установку зависимостей

Устанавливаем зависимости:

```
pip3 install requests
pip3 install furl
pip3 install ticket_parser2 -i https://pypi.yandex-team.ru/simple
```

Если установка ticket_parser2 не работает, дело может быть в слишком новой версии питона. Можно попробовать установить более новую версию:

```
pip install ticket_parser2_py3 -i https://pypi.yandex-team.ru/simple
```

После этого, можем просто запустить:

```
python3 taxi/logistic-dispatcher/tools/qa-knife/main.py
```

### Настраиваем быстрый доступ

Получаем путь к инструменту:

```
echo `pwd`/taxi/logistic-dispatcher/tools/qa-knife/qa-knife
```

Или в случае второго варианта установки:

```
echo python3 `pwd`/taxi/logistic-dispatcher/tools/qa-knife/main.py
```

И добавляем токен для tvm и alias-ы в .bashrc для доступа из любого места на машинке:

```
vim ~/.bashrc
Gi

export tvm_2020943=<токен, за которым надо обратиться к @skulik>
alias qa-knife='<результат выполнения прошлой команды>'

<esc>:wq!
```

Применяем все изменения из .bashrc

```
source ~/.bashrc
```

Всё, можно пользоваться!

## Использование

Запуск:

```
qa-knife
```

### Параметры

#### --flow

Единственный обязательный параметр. Принимает одно из двух значений:
* pull, тогда заявка будет создана для флоу pull dispatch в лавке 
* regular, тогда заявка будет создана по обычному флоу

#### --target-contractor-id

Опциональный параметр. Можно указать id своего курьера в формате dbid_uuid, тогда заявка будет назначена именно на этого курьера.

#### --num-orders

Число заявок, которые нужно создать. Удобно, если нужно сделать батч.

#### --corp-client-id

id корпклиента. По умолчанию используются 
* тестовый корпклиент Еды: b8cfabb9d01d48079e35655c253035a9 (flow regular)
* тестовый корпклиент Лавки: 63f14a6fcce64e4d9ca49ad6958ababf (flow pull)

#### --claim-kind

Параметр, специфичный для заказов Еды и Лавки.
* plarform_usage: заявка создается по четырем классам, использование карго и диспатча как платформы
* delivery_service: заявка создается по двум классам, использование карго и диспатча как заказа такси-курьера

По умолчанию plarform_usage.

#### --due-from-now

Отступ в секундах от момента "сейчас" для целевого времени подачи. По умолчанию 120.

#### --target-logistic-group

Требуемая логистическая группа. Актуально только для фудтеха.

#### --target-meta-group

Требуемая метагруппа. Актуально только для фудтеха.

#### --force-no-batch

Bool. Запретить батчить созданный заказ с каким угодно другим (использование: `--force-no-batch true`).

### Примеры

Создать батч из двух заказов по обычному флоу на заданного курьера:

```
qa-knife --flow regular --num-orders 2 --target-contractor-id 0253f79a86d14b7ab9ac1d5d3017be47_5448b78cc06eecd80e02082e904ae45b
```

Создать заказ по флоу pull-dispatch

```
qa-knife --flow pull
```

Вывод содержит ссылку для быстрого перехода на тестовую админку карго:

```
Claim created: https://tariff-editor.taxi.tst.yandex-team.ru/corp-claims/show/f6c338ac11eb452e97846b185fdf6a21/info
Claim f6c338ac11eb452e97846b185fdf6a21 confirmed
```
