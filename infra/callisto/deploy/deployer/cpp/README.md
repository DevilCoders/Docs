# Deployer, driven by dynamic tables

### Запуск
Предполагается, что деплоер запускается в поде deploy на правах сайдкара (todo: что это значит?).
После запуска деплоер отвечает на readiness-пробу отрицательно до тех пор,
пока не докачает себе *определенный* процент запланированных на этот под ресурсов.
Liveness-проба успешна с момента запуска.
Детали <https://wiki.yandex-team.ru/deploy/docs/concepts/pod/workload/probes/#motivacijanezavisimojjrabotyi>

### Cluster membership
Контроллеру необходимо идентифицировать не просто под, но под, материализованный на ноде.
К примеру, при переезде пода на другую ноду контроллер хочет перепланировать ресурсы с этого пода на другие,
а не дожидаться, когда переехавший под накачает себе все старые ресурсы.
Для RS под, материализованный на ноде, идентифицируется парой (node id, pod id).
Для раскладки шардов это избыточно, идентификация будет другая.

### Design
message TPodTarget {
    string PodId = 1 [(NYT.key_column_name) = "PodId"];
    string Namespace = 2 [(NYT.key_column_name) = "Namespace"];
    string LocalPath = 3 [(NYT.key_column_name) = "LocalPath"];

    TSource ResourceSpec = 5;
    TNotification Notification = 6;
}


class TTaskManager {
public:
    //
};
