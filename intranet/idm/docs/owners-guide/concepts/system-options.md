# Приложение 2. Опции системы

При подключении системы к IDM можно указать опции, согласно которым система будет работать:

## Опция «Включена» {#system-on}

#|
||Состояние: установлена | Состояние: не установлена||
||Система находится в активном состоянии. В активной системе можно запрашивать, подтверждать и отзывать роли. | IDM переводит систему в неактивное состояние.

При этом система исчезает из списка [IDM. Все системы](https://idm.yandex-team.ru/systems) и становится недоступна в форме запроса роли.||
|#

## Опция «Может быть сломана» {#can-be-broken}

#|
||Состояние: установлена | Состояние: не установлена||
||Если во время сверки таблицы ролей IDM и таблицы системы обнаружено более пяти [неконсистентностей](close-neconsist.md), IDM выполняет несколько действий:

- Отправляет в систему уведомление об обнаруженных неконсистентностях. Разрешить неконсистентности должны ответственные за систему.
- Отключает систему и отправляет об этом уведомление ответственным за систему. В сломанной системе нельзя запрашивать, подтверждать и отзывать роли. | IDM отправляет в систему только уведомление об обнаруженных неконсистентностях.

Разрешить неконсистентности должны ответственные за систему.||
|#

## Опция «Сломана» {#broken}

#|
||Состояние: установлена | Состояние: не установлена||
||IDM отключает систему и отправляет об этом уведомление ответственным за систему. Отключенная система доступна в форме запроса роли, однако в ней нельзя запрашивать, подтверждать и отзывать роли. | Система находится в активном состоянии: можно запрашивать, подтверждать и отзывать роли.||
|#

## Опция «Имеет регулярный пересмотр» {#review}

#|
||Состояние: установлена | Состояние: не установлена||
||IDM запускает механизм пересмотра ролей каждые 365 дней.

Если роль обновлялась 365 дней назад:

1. Переводит роль в состояние «Перезапрошена».
1. Запрашивает роль повторно, применяя workflow системы. Роль переходит в состояние «Запрошена».Роль необходимо подтвердить в течение 14 дней, в противном случае роль отзывается.

Ответственный за систему может изменить периодичность пересмотра ролей. Для этого необходимо написать запрос на рассылку [tools@yandex-team.ru](tools@yandex-team.ru). | IDM не запускает механизм пересмотра ролей.

Отключать опцию рекомендуется для систем с большим количеством ролей и пользователей (например, CAuth или Staff).||
|#

