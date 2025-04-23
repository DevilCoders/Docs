# Authentication
Для аутентификации внутренних пользователей сервисы в RTC используют внутренний паспорт (a.k.a. blackbox). Для авторизации же используется
staff (принадлежность пользователя к группами staff/abc).

Для аутентификации есть два аспекта:
  * cookie - для доступа через браузер (кастомные UI и kubernetes dashboard)
  * token - для доступа через API и kubectl

Посмотрев на различные варианты **пока** остановились на 
  * штатном kube-apiserver
  * [webhook'ах](https://kubernetes.io/docs/reference/access-authn-authz/authentication/#webhook-token-authentication)

Мотивация:
  * новый встроенный аутентификатор: нужен fork [kubernetes/kubernetes](https://github.com/kubernetes/kubernetes) - высокий порог входа и поддержки.
  * authenticating proxy - нужно уметь работать с длинными запросами (watch'и), находится на критичном пути запроса - высокий порог входа

Реализация: [kube-auth-webhook](https://a.yandex-team.ru/arc/trunk/arcadia/infra/kube-auth-webhook/).

Дальнейшие шаги:
  * написание контроллера, который будет складывать YandexUser crd из стаффа {name: nekto0n, uid: x, groups: []}.
