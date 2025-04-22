# Разбор проблем с необновляющейся ТС(пока только для java)

## Не выкладывается на 1 под, на остальное выехало нормально
В этом случае проще эвакуировать под по [инструкции](../howto-redeploy-pod.md)


## Выкладка упала по таймауту после завершения сборки
Падание по таймауту обычно выглядит так:
1. Запускаем `direct-release`
2. Фаза сборки проходит нормально, и начинается фаза выкладки `### current cmd: test-update`
3. `sleeping for 30 seconds...` пишется еще целый час, а потом утилита падает с ошибкой, например такой:
```
Timed out. See dctl list deploy_ticket --release-rule direct-logviewer-test-rule |grep SANDBOX-1103897965-testing-direct-logviewer-test-rule for current status
cmd failed, stop (['dt-update-yadeploy-stage', '--stage', 'direct-logviewer-test', '--deploy-ticket', u'SANDBOX-1103897965-testing-direct-logviewer-test-rule', '--wait'])
message to send:
== direct-release ==
java-logviewer/testing/create-release: FAIL
Signal 0, exit code 1
Duration: 01:38:55
```
В этом случае можно сначала посмотреть статус деплоя приложения командой, предложенной в упавшем выводе. Там есть такая строчка:
```
Timed out. See dctl list deploy_ticket --release-rule direct-logviewer-test-rule |grep SANDBOX-1103897965-testing-direct-logviewer-test-rule for current status
```
Набираем в терминале
```
dctl list deploy_ticket --release-rule direct-logviewer-test-rule |grep SANDBOX-1103897965-testing-direct-logviewer-test-rule`
```
И видим, что статус действительно `InProgress`:
```
WARNING! Current dctl version is outdated. Please update dctl to the last version using this instruction https://wiki.yandex-team.ru/deploy/docs/dctl/.
| SANDBOX-1103897965-testing-direct-logviewer-test-rule | direct-logviewer-test | SANDBOX-1103897965-testing | direct-logviewer-test-rule | InProgress |
```
Если это так, то идем в Yandex.Deploy [в проект direct-np](https://deploy.yandex-team.ru/projects/direct-np) и ищем там стэйдж с нашим выкладываемым приложением.
Его название будет начинаться как наше приложение, с суффиксом `-testing`, и статус его будет `in progress` с мигающей синей точкой, например так:

<img src="https://jing.yandex-team.ru/files/vamenshov/direct_np_stage.79a5772.png" alt="stage" width="1000" />

Заходим в стэйдж нашего приложения:

<img src="https://jing.yandex-team.ru/files/vamenshov/deploy-pod.a72e943.png" alt="pod" width="1000" />

Видим, что один из подов упал (1), перебираем какой из них (2), пока не найдем под со статусом `dead` (3). Кода нашли,
то кликаем в саму серую плашку пода, но ни в коем случае, не попадаем ни в какие записи внутри нее:

<img src="https://jing.yandex-team.ru/files/vamenshov/pod_gray.7718930.png" alt="pod line" width="1000" />

Откроется дополнительная панель, из которой нужно будет скопировать строку для доступа на машину пода по SSH. Для этого
нужно кликнуть мышкой по иконке копирования напротив SSH по строке `Box` с именем нашего приложения и суффиксом `-box`.

<img src="https://jing.yandex-team.ru/files/vamenshov/pod_ssh.ba7dc86.png" alt="pod" width="1000" />

Затем заходим на машину пода из терминала по скопированной команде и запускаем там, например `htop`.
В `htop` может быть видно, что приложение стартует, что-то пытается активно делать, и через несколько секунд падает. Потом поднимается снова и опять падает.

Чтобы понять, почему оно падает, нужно открыть логи `messages - New-style messages of all direct systems` через [тестовое веб-приложение логвьювера](https://test-direct.yandex.ru/logviewer/).
При этом в поле `Range` нужно указать диапазон времени, когда приложение падало на сбойном поде (то есть текущее, так как падает оно у нас прям сейчас),
а в поле `service` указываем имя нашего приложения с префиксом `direct.`, [например вот так](https://test-direct.yandex.ru/logviewer/short/vOU1AfNV4NdKoH). Далее ищем в логах сообщения об ошибках
и устраняем проблему.

При этом, если мы выкладываем сам logviewer, то логи его падения все равно будут доступны, через оставшиеся рабочие экземпляры программы на других подах.

## Выкладка упала по бюджету на обновлении, т.к. приложение падает
* Найти обновляемый стейдж
* Найти обновляемый под
* Зайти в под
* Убедиться, что приложение рестартует(по ssh), может оказаться, что конкретный pod не очень и тогда его проще починить по пункту выше
* Пойти посмотреть в логи в [тестовом логвьювере](https://test-direct.yandex.ru/logviewer) в messages, отфильтровав, например по имени пода
* Устранить проблему

## Не релизится для деплоя свареный ресурс
Попытки зарелизить сендбочий ресурс заканчиваются ошибкой вида
```
400 Client Error: BAD REQUEST for url
внутри которой
"Access denied. User ppc cannot release resource #<номер ресурса>, type YA_PACKAGE. To fix this, you should add this user to 'releasers' property of this resource"
```
Здесь проблема, что, скорее всего, приготовился ресурс типа YA_PACKAGE. Убедиться можно на странице таски. Это произошло из-за того, что direct-release не распознал тип приложения и запустил таску без нужных параметров. Поправить руками тип ресурса можно в зукипере следующей командой `dt-zkcli -H ppctest-zookeeper01i.sas.yp-c.yandex.net:2181 vim /direct/release-state/<стейдж (stable/testing/waitng)>/<приложение>[/1 если это waiting]`
Получится дифф вида:
```diff
--- zk
+++ edited version
@@ -22,6 +22,6 @@
-    "release_type": "",
+    "release_type": "java_yadeploy",
```

## Не грузится бета с ошибкой "Сервис временно недоступен" { #beta-unavailable }

Пусть `$NNNN` - номер беты.

Выглядит ошибка примерно так: При заходе на `https://$NNNN.beta1.direct.yandex.ru` видим примерно следующее:

<img src="https://jing.yandex-team.ru/files/vamenshov/beta_service_unavailable.035067b.png" width="1000" alt="Сервис временно недоступен">

Как чинить:

1. Определяем имя ppcdev, (пусть он будет `$ppcdevX`) на котором находится бета. Алгоритм такой:
   - Если номер беты состоит из 4-х цифр, берем первую.
   - Если из пяти - первые две.
   - Вычитаем из полученного числа 7.
   - Добавляем результат к `ppcdev`.
   - То есть для беты `8998` берем первую цифру - `8`, вычитаем `7`, получаем `1`. Значит она на `ppcdev1`. А для беты `13679` берем первые две цифры - `13`, вычитаем `7`, получаем `6`, значит она на `ppcdev6`.
2. Заходим на `$ppcdevX` с локальной машины
    ```shell
    ssh $ppcdevX # не забудьте заменить $ppcdevX на настоящее имя ppcdev
    ```
3. Заходим в папку самой беты
    ```shell
    b $NNNN # не забудьте заменить $NNNN на номер беты
    ```
4. Смотрим, запущен ли apache
    ```shell
    ps aux | grep apache | grep $NNNN # не забудьте заменить $NNNN на номер беты
    ```
   Если вывод пустой, значит `apache` на запущен
5. Если не запущен, смотрим, под кем смонтирована бета
    ```shell
    ls -lAh
    ```
    в выводе будет что-то типа
    ```shell
    total 750K
    -rw-r--r--   1 ppc ppc  12K Jul 23  2020 .arcignore
    -rw-r--r--   1 ppc ppc  974 Aug  8  2019 .complete
    -rw-r--r--   1 ppc ppc 9.6K Jul 23  2020 .gitignore
    -----------//-------------------------//-----------
    ```
   Берем пользователя из третьей колонки (пусть он будет `$beta_user`), в данном примере он `ppc`
6. Перезапускаем `apache` под найденным пользователем командой
    ```shell
    sudo -u $beta_user direct-mk apache-restart  # не забудьте заменить $beta_user на имя пользователя беты
    ```
7. Если пишет, что нет прав, обращаемся к коллегам за помощью, например права есть у [дежурных](https://abc.yandex-team.ru/services/direct-app-duty/duty).
8. Если `apache` запущен, смотрим лог
    ```shell
    tail apache/logs/error.log
    ```
9. Смотрим, в каком файле ошибка возникает.
10. Так же можем посмотреть ошибки в логах через [тестовый logviewer](https://test.direct.yandex.ru/logviewer/short/XY5OCbgy4UhACs), указав в качестве сервиса `direct.perl.web`
11. Идем в [репозиторий перлового кода директа в Аркануме](https://a.yandex-team.ru/arc/trunk/arcadia/direct/perl) и ищем, кто последний раз правил файл, на котором все падает.
12. Пишем автору исправления, что так и так, поправь, пожалуйста.
13. Если автор не может оперативно поправить ошибку, а в чем дело понятно - правим сами новым pr-реквестом и мерджим.
14. Если проблема совсем непонятная, можно попробовать пересобрать бету. Для этого нужно выполнить следующие команды:
    ```shell
    b $NNNN # не забудьте заменить $NNNN на номер беты
    sudo -u $beta_user direct-mk up  # не забудьте заменить $beta_user на имя пользователя беты
    ```
15. Если не помогло, обращаемся к коллегам за помощью, в первую очередь можно спросить [дежурных по релизам и тестовой среде](https://abc.yandex-team.ru/services/direct-app-duty/duty2/30726), а если они не смогут помочь, то можно обратиться к [дежурным по продакшену](https://abc.yandex-team.ru/services/direct-app-duty/duty2/30725).

## Другие проблемы

{% note tip %}

Раздел будет дополняться, мы открыты к пулл-реквестам в доку

{% endnote %}
