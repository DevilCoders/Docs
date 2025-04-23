## Библиотека предоставляет возможность организации обработки вызовов посредством **Controller**

**Controller**
Класс, умеющий обрабатывать request и сохраняющий результат внутри себя

**Request**
Класс/структура внутри contoller описывающая параметры вызова

**BaseController**
Базовый класс для всех контроллеров с виртуальными методами которые необходимо реализовать в порожденных
и за счёт которых делаются все обработки схожим образом

## Как пользоваться

### Базовый вариант

Реализовать класс своего контроллера породив от шаблона BaseController

```
namespace custom_ns {
class CustomController;
} // namespace custom_ns

namespace maps::wiki::controller {
template<>
struct ResultType<custom_ns::CustomController>
{
    std::string result;
};
} // namespace maps::wiki::controller

namespace maps::wiki::custom_ns {
class CustomController : public controller::BaseController<CreateReview>
{
public:
    struct Request
    {
        std::string dump() const;
        std::string param1;
        std::string param3;
    };

    CustomController(const Request& request, taskutils::TaskID asyncTaskID);

    std::string printRequest() const override { return request_.dump(); };
    static const std::string& taskName();
protected:
    // Тут выполняются все действия контроллера
    // Экземпляр Request доступен как request_
    // Экземпляр Result хранится по адресу из переменной result_
    void control() override;

private:
    const Request request_;
};

} // custom_ns
```

Вызов оператора `()` у экземляра приводит к выполнению кода и появлению результата

### Асинхронное выполнение

Сам по себе базовый вариант не очень интересен.
Его основное назначение это создать контроллер, который можно выполнять асинхронно.
При этом контроллер запускается и наружу отдаётся token по которому можно опрашивать готовность результата выполнения
Статус и результат записываются в базу.

Как использовать

1 Подготовить настройки поддержки асинхронного выполнения. Класс **AsyncTasksSupport**
Настройки описывают соединение с базой где хранятся статусы выполения (для taskutils) и threadpool

2 Описать контроллер, который принимает другой контроллер как аргумент шаблона и запускает его асинхронно.
Простой пример: ```maps/wikimap/mapspro/services/social/src/api/feedback_review/controller_async.h```
**ControllerAsyncTaskContext** управляет контекстом выполнения
**ControllerAsync** реализует передачу упраления и получение результата запуска как обычный контроллер.

3 Реализовать обработку запроса на получение результата
Контроллер **AsyncTaskResult** для обработки запроса реализован в библиотеке
Например
```
YCR_RESPOND_TO("GET /results/$")
{
    const auto& asyncTasksSupport = Globals::asyncTasksSupport();
    const auto& tokenSecretWord = asyncTasksSupport.manager().tokenSecretWord();
    auto asyncTaskResult = std::make_unique<controller::AsyncTaskResult>(
        taskutils::Token(
            positionalParam<std::string>(argv, 0),
            tokenSecretWord));
    asyncTaskResult->load(asyncTasksSupport);
    makeJsonResponse(response, asyncTaskResult->toJson());
}
```
