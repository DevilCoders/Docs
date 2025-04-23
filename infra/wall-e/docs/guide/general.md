# Wall-E: The Guide

Wall-E работает только с теми хостами, которые в него добавлены.

В качестве наливаек поддерживаются [LUI](https://setup.yandex-team.ru/) и [Einstellung](https://eine.yandex-team.ru/).

Для работы с Wall-E доступны: [Web-интерфейс](#ui), [CLI](#cli) и [REST API](#api).

## UI {#ui}

UI для работы с Wall-E доступен по основному адресу: [https://wall-e.yandex-team.ru](https://wall-e.yandex-team.ru)

Для использования Wall-E отдельной документации не требуется. UI является основным интерфейсом к Wall-E, однако новый функционал, как правило, поддерживается в cli раньше, чем в UI на несколько недель.

## API {#api}

Документация на API находится [здесь](http://api.wall-e.yandex-team.ru/).

В качестве клиента к API предлагается использовать [python-sdk](https://a.yandex-team.ru/arc/trunk/arcadia/infra/wall-e/sdk) в аркадии ([пример использования](https://a.yandex-team.ru/arc/trunk/arcadia/infra/wall-e/client)) или модуль [wall-e.api](https://pypi.yandex-team.ru/dashboard/repositories/default/packages/wall-e.api/) из PyPI (в последнем случае при добавлении клиента в зависимости к своим пактам рекомендуется привязываться к его major-версии, т. к. она будет меняться при каждом релизе, ломающем обратную совместимость).

Для получения OAuth-токена для запросов пройдите по [этой ссылке](https://oauth.yandex-team.ru/authorize?response_type=token&client_id=9e9702c0b7f54152ac339989d9039ccd).

## CLI {#cli}

Документация по использованию cli собрана [в отдельной секции](../cli.md).


## Информация для инженеров и администраторов машин {#host-maintenance}

Если вам нужно что-то сделать руками с машиной, которая находится под управлением Wall-E (к примеру, отправить в преднастройку в [Einstellung](https://wiki.yandex-team.ru/einstellung)), то прежде чем выполнять какие-либо действия, необходимо сообщить об этом Wall-E - иначе он может посчитать, что с машиной что-то не так, возможно попробует ее ребутнуть или переналить. Это плохо как нам - переналить у него машину, скорее всего, не получится, он посчитает ее мертвой, и на следующий день дежурный администратор будет ломать себе голову, что же такое случилось; так и вам - преднастройку машинка тоже, скорее всего, не пройдет (или пройдет не с первого раза), т. к. Wall-E будет ребутать машину в середине Eine'вского этапа.

Чтобы избежать всех этих проблем, просьба:

Перед тем, как что-либо делать с машиной, посмотрите, работает ли она под управлением Wall-E и если да - то [переведите ее в `maintenance state`](maintenance.md):
`$ wall-e hosts set-maintenance $host --ticket TICKET --ttl 2d -r "host needs maintenance"`

Переводя машину в `maintenance state`, вы сообщаете Wall-E о том, что с данного момента машина находится под вашим личным контролем, и, несмотря на то, что он будет продолжать мониторить текущее состояние этой машины, никаких автоматических действий над ней он предпринимать не будет.

{% note tip %}

Если коллега, который перевёл машину в этот статус, ушёл в отпуск, а вам надо продолжить работу с машиной, добавьте ключ `--ignore-maintenance` чтобы Wall-E понял, что вы знаете, что делаете.

{% endnote %}


## Конфигурация стендов Wall-E {#stand-config}
* Production:
   * [UI](https://wall-e.yandex-team.ru/)
   * [API](http://api.wall-e.yandex-team.ru/)
   * CLI-команда для работы со стендом: `wall-e ...`
   * [Активная конфигурация сервиса](http://api.wall-e.yandex-team.ru/config)
   * [Мониторинг](https://yasm.yandex-team.ru/template/panel/wall-e-metrics/ctype=prod)
   * [Sentry](https://sentry.t.yandex-team.ru/monitoring/wall-e-production/)
* Testing:
   * [UI](https://wall-e-test.yandex-team.ru/)
   * [API](http://api.wall-e-test.yandex-team.ru/)
   * CLI-команда для работы со стендом: `wall-e --testing ...`
   * [Активная конфигурация сервиса](http://api.wall-e-test.yandex-team.ru/config)
   * [Мониторинг](https://yasm.yandex-team.ru/template/panel/wall-e-metrics/ctype=test)
   * [Sentry](https://sentry.t.yandex-team.ru/monitoring/wall-e-prestable/)


### Конфигурация сервиса {#service-config}

Конфигурация сервиса определяется конфигом, который лежит в репозитории вместе с исходным кодом. Описание всех опций в конфиге можно посмотреть в [дефолтном конфиге](https://a.yandex-team.ru/arc/trunk/arcadia/infra/walle/server/walle/walle.conf.yaml) (там есть комментарии практически ко всем опциям).

Каждый инстанс Wall-E по `/config` отдает конфиг, с которым он запущен в данный момент. В разделе [конфигурация стендов](#stand-config) приведены ссылки на активную конфигурацию для каждой инсталляции.


## E-mail-нотификации

Если вы хотите получать на почту уведомления обо всех операциях над хостами всех проектов, либо об ошибках при выполнении этих операций, либо чтобы вы стояли в копии всех заявок в Бот, которые создает Wall-E, обратитесь в ((mailto:wall-e@yandex-team.ru рассылку)).


## В крайних случаях {#how-to-kill-wall-e}

Если вдруг Wall-E совсем сойдет с ума и начнет уничтожать кластер, несмотря на все внутренние защиты, то для того, чтобы гарантированно остановить его, необходимо пройтись по инстансам сервисов, собраных [на этом дашборде в няне](https://nanny.yandex-team.ru/ui/#/services/dashboards/catalog/wall-e/). Для надежности после деактивации стоит на всякий случай проверить, что `ps aux | egrep 'wall-e|walle'` дает пустой вывод.


## Контакты {#contacts}

По всем вопросам и хотелкам просьба писать в [стартрек](https://st.yandex-team.ru/WALLESUPPORT) или [на рассылку](mailto:wall-e@yandex-team.ru) (которая тоже форвардит письма в трекер).

Если случилось что-то экстренное – свяжитесь напрямую с [нашей командой](https://abc.yandex-team.ru/services/wall-e/duty/).
