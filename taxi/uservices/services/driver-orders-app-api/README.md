## Codestyle

Основные документы, описывающие CodeStyle:
* https://wiki.yandex-team.ru/taxi/backend/codestyle-and-checklist/
* https://wiki.yandex-team.ru/taxi/backend/dev-review-rules/

Некоторые вещи в них не формализованы, поэтому хочется явно пояснить их.

В случае спорных моментов, касающихся языка С++, стоит обратиться к следующим источникам, в порядке приоритетов:
* https://isocpp.github.io/CppCoreGuidelines/CppCoreGuidelines
* Можно посмотреть гайдлайны крупных проектов, например Chromium guildelines: https://www.chromium.org/developers/smart-pointer-guidelines
* блоги известных людей, stackoverflow

### Пояснения

* Для fwd decl используется следующий стиль:
  ``` 
  namespace handlers {
  struct Dependencies;
  }  // namespace handlers 
  ```
  * Здесь делается выбор в пользу лаконичности, нежели "читабельности" - не добавляются пустые строчки после `namespace {`

* Всегда используются импорты по полному пути: `#include <models/some_header.hpp>`
  * Очевидное исключение -- в парном .cpp-файле первым должен идти соответствующий заголовочный файл в ""
* Структура папок должна отражать `namespace`, используемый в файле:
  * https://wiki.yandex-team.ru/taxi/backend/codestyle-and-checklist/#uservicesonly пункт 3.2
  * т.е. файл по пути `src/models/order/request.hpp` должен содержать `namespace models/order { ... }` 
* Внутри `src/` принимаются следующие папки со своей логикой:
  * `clients` -  клиенты (обёртки на сгенерированными клиентами) по работе с внешними сервисами
  * `stq` - код по обработке STQ-очереди
  * `views` - работа со слоем представления, т.е. с тем, что отдается пользователю. В целом, существенная часть 
  этого отдается на откуп кодогенерации, поэтому "вьюхи" обычно достаточно "тонкие".
  * `models` -  основная бизнес-логика по работе с данными + сами эти данные. В идеале, эта часть должна быть отвязана от view/HTTP-специфичных вещей
