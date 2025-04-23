# Requests

В плагине `requests.php` размещаются разнообразные функции, которые запускаются из view устройства в Racktables. Например, секция **summary - Прочее** для устройства формируется тут.

Для того, чтобы добавить что-то в **summary** надо:
- добавить Hook: `registerHook ('modifyEntitySummary', 'addTestButton', 'chain');`
  - `modifyEntitySummary` - не меняем
  - `addClearKnownHostsBtn` - имя callback
  - `chain` - не меняем
  - про registerHook можно почитать код в <https://noc-gitlab.yandex-team.ru/nocdev/racktables-upstream/-/blob/master/wwwroot/inc/functions.php>
  - если не добавить registerHook, то функция `addTestButton` не отработает
- добавить функцию `addTestButton`
  ```php
    function addTestButton($summary, $object) {
        if (empty ($summary['{sticker}Прочее'])) {
            $summary['{sticker}Прочее'] = '';
        }
        $summary['{sticker}Прочее'] .= <<<END
    <a target="_blank" href="https://yandex.ru/pogoda/moscow?lat=55.753215&lon=37.622504">Погода в Москве</a>
    END;

        return $summary
    }
  ```
- стоит учитывать, что функция возвращает `$summary`, потому что блок **Прочее** находится в **summary**, поэтому стоит придерживаться этого именования переменной.

Результат: Теперь вы можете смотреть погоду в Москве из RT

![img1](./_images/requests/img1.png)


