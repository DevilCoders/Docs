# Документация InvAPI

## Описание

InvAPI - это API на GraphQL над инвентарными системами, используемыми Отделом Сетевой Инфраструктуры.

InvAPI доступен по ссылкам:  
 - [Чтение]({{ urls.invapi-ro }}) 
 - [Чтение и запись]({{ urls.invapi-rw }}) 

Описание текущей схемы полей и объектов можно найти в `GraphiQL` в плашке справа с документацией.  

Graph**i**QL - a graphical interactive in-browser GraphQL IDE for testing endpoints  

Исходники текущей версии расположены:  
 - <https://noc-gitlab.yandex-team.ru/nocdev/rtapi2rr>

Аутентификация:  
 - Oauth: <http://oauth.yandex-team.ru/authorize?response_type=token&client_id=950f303bdd4446f3870c8d4156a1c1c9>
 - TVM: <https://abc.yandex-team.ru/services/NOCDEV/resources/?view=consuming&layout=table&supplier=14&show-resource=18842985>

Клиентские библиотеки:
 - Golang: [Link to Arc](https://a.yandex-team.ru/arc/trunk/arcadia/noc/go/invapi)

Примеры использования в коде:  
 - Python (Pahom): [Link to Arc](https://a.yandex-team.ru/arc/trunk/arcadia/noc/pahom/bin/confsyncd)
 - Golang (Alexandria): [Link to Arc](https://a.yandex-team.ru/arc/trunk/arcadia/noc/alexandria/internal/adapters/alexandria/invapi)

 **Технический менеджер**: [Воловик Вадим](https://staff.yandex-team.ru/vdvolovik)

 **Ведущий разработчик** [Константин Сазонов](https://staff.yandex-team.ru/moonug)
 
## Q&A

**Вопрос:** Какая цель проекта?  
**Ответ:**  
   - Создание полноценного API для Racktables, которое не будет просто выставлять кишки реализации Racktables наружу, а обеспечит необходимый уровень абстракции и изоляции.  
   - Возможные бонусы: уменьшение нагрузки на RT, уменьшение времени на создание новых и поддержку старых ручек в RT (перестать создавать новые php-ручки и выпиливать старые). Необходимый пререквизит для распила монолита RT.  

**Вопрос:** Чем InvAPI лучше RTAPI для клиентов?  
**Ответ:**  
   - GraphQL это понятный API с заданной схемой, который доступен через POST HTTP запросы. Нет в общем случае необходимости в поддержке клиентов со специализированной авторизацией и прочими особенностями почти JSON-RPC RTAPI.  
   - Для получения необходимой информации в InvAPI GraphQL нужно сделать меньше запросов для получения информации (один запрос). Сбор и подготовка информации для ответа клиенту выполняется на стороне сервера, что позволяет пересылать меньше данных и лишних ненужных полей.  

**Вопрос:** Почему был выбран GraphQL? Для новых проектов в nocdev рекомендуется gRPC.  
**Ответ:**  
   - Большая часть запросов к RT это получение информации. Так как в RT огромное количество данных, то большая часть клиентов наталкивается либо на избыток данных в текущих ручкам, либо на их недостаток. Из распространенных сейчас решений эта проблема в явном виде решена только GraphQL.  
   - Преимущества описанные выше для клиентов  
   - Возможность не создавать много разрозненных ручек и отдавать фильтрацию необходимых полей в ответе на сторону клиента, что облегчает поддержку и развитие  
   - Возможность объединять запросы из разных ручек в один ответ в сторону клиента  

**Вопрос:** Как будут передаваться схемы между проектами? Для gRPC(для протобафов) есть тулинг в аркадии  
**Ответ:**  
   - GraphQL не подразумевает передачу схемы в общем случае, поскольку является самоописательным. Но в нашей реализации изменения схемы отслеживаются в репозитории в явном виде и текущую схему всегда можно получить тут
   - для python и golang планируется написать специальных клиентов для упрощения жизни разработчикам. Но строго говоря обязательными они не являются. GraphQL можно использовать хоть через curl из терминала.

**Вопрос:** Весь функционал RTAPI переедет в GraphQL? Когда?  
**Ответ:**  
   - Формально говоря, не весь, так как через RTAPI доступен вызов почти 3000 php-функций. Поддерживать все это разнообразие нет смысла. Да и InvAPI создается как отвязанный от совсем уж подробностей реализации чего-бы то ни было в Racktables.
   - Планы в NOCTODO-247 
