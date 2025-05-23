## Бизнес-задача

Реализовать минимальный функционал колл-центра в международной диспетчерской Yango Fleet: сотрудник принимает звонок в UI диспетчерской, и в форме создания заказа происходит автозаполнение полей, значения которых для позвонившего пользователя известны системе.

Колл-центр уже существует как отдельный продукт и имеет более чем достаточный для наших целей функционал. Поэтому для экономии сил и времени хочется переиспользовать его в Yango Fleet.

## Проблема

Бэкенд колл-центра закрыт authproxy-сервисом, отличающимся от fleet-authproxy, поэтому сейчас фронтенд диспетчерской не может ходить в сервисы колл-центра.

## Решение

Одно из возможных решений заключается в синхронизации пользователей (и их ролей) диспетчерской и колл-центра.

## Интеграция

### Система прав доступа колл-центра

Доступ поделен на проекты. В каждом проекте своя система ролей. Пользователь не привязан к проекту, создается отдельно, и ему присваиваются необходимые роли с доступами в нужные проекты. То есть пользователь может иметь несколько ролей, в том числе и в разных проектах. Пользователь идентифицируется по yandex UID'у.

Ситема проверки прав единая для yandex- и yandex_team-пользователей. Авторизация происходит в authproxy-сервисе по UID'у. По нему же хранятся роли для обоих типов пользователей.

### Синхронизация

Парк в диспетчерской будет соответствовать проекту в колл-центре. Роль пользователя в парке - роль пользователя в проекте колл-центра.

При создании колл-центра на их стороне отрабатывает скрипт, запускающий процесс. На каком-то этапе создания колл-центра для парка скрипт будет дергать нашу ручку, сообщая тем самым, что для конкретного парка включается возможность использования функционала колл-центра через конкретный проект. Затем пользователи этого парка начинают синхронизироваться с пользователями проекта колл-центра.

При отключении колл-центра парка так же будет дергаться наша ручка, сообщая, что синхронизацию для конкретного парка нужно прекратить.

Сама синхронизация будет осуществляться периодической таской. Для маппинга нам нужны идентификаторы проекта и ролей. Получать их можно через ручку включения синхронизации. В парке с включенной синхронизацией периодически будут отлавливаться недавно созданные и отредактированные пользователи и синкаться с пользователями и ролями проекта колл-центра. Так как в колл-центре пользователи не привязаны к проекту, могут быть повторные запросы с одинаковыми UID'ами.

*Возможно, стоит начать хранить в postgres'е UIDы пользователей, чтобы не делать за ними дополнительный запрос в dispatcher-access-control. В любом случае при переезде юзеров из redis'а это поле должно появиться.*

*Синхронизация yandex_team-пользователей. Тут пока непонятно. У yandex-team'ов есть роли в диспе, они хранятся в redis'е списком логинов пользователей для каждой роли. Кажется, что нам все они не нужны в колл-центре, поэтому можно в проектах создавать одну отдельную роль для yandex-team'ов, которая будет readonly, например. Но тут еще вопрос в том, как этих пользователей создавать, потому что, если я все правильно понял, UIDы балково мы не можем достать по логинам. Есть в библе паспорта метод, вытягивающий инфу о юзере по email'у, но там нужен ip. Как одно из возможных решений, можно при запросе к функционалу КЦ из диспы при нехватке прав, то есть не созданном в КЦ сотруднике, предлагать его создать. Не очень клиентоориентировано, но легко реализуемо + не нужно будет создавать лишних сотрудников в КЦ. Или можно попытаться скрыть это создание.*

### Детали реализации

Требуется разработка:

1. Ручка включения синхронизации парка с КЦ `/v1/sync/call_center/park/on` в сервисе `fleet-access-control-synchronizer`;

1. Ручка выключения синхронизации парка с КЦ `/v1/sync/call_center/park/off` в сервисе `fleet-access-control-synchronizer`;

3. Внутренняя ручка списка пользователей в парке `/v1/users/list` в сервисе `fleet-users`.

3. Периодическая таска в сервисе `fleet-access-control-synchronizer` для синхронизации парков, ролей, пользователей и их прав.

API для создания и редактирования пользователя в колл-центре предоставяется командой колл-центра.
