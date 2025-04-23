# Stapler v1

## Task
Основной класс для описания полезной нагрузки (исполняемого кода) кубиков в `Nirvana`

## Context
Контекст

## Stapler
Класс для генерации и публикации графов

## Использование результатов инстансов Task
В "обвязке" для исполнения кода `stapler_app_runner` указан один обязательный текстовый выход `result`.

На каждый вызов run возвращается объект `OpCallResult`
Про него можно подробнее почитать здесь -> `https://a.yandex-team.ru/arc/trunk/arcadia/nirvana/valhalla/docs/reference/op_call_result.md`
Каждый объект класса `Task` или его наследников принимает обязательный параметр output, но указывать его не нужно.
output - по сути это имя файла куда записывается результат операции. Запись результата определена в методе _`after_run` класса `Task`
Использовать его или нет решают разработчики графа. Но это очень удобная и полезная опция.

## Специальные кубики `Nirvana`

### app_runner
Для запуска кода (приложения) калькулятора на основе `Stapler`
- [app_runner readme](./nirvana/app_runner/README.md)

### gpu_app_runner
Для запуска кода torch тасок
- [gpu_app_runner readme](./nirvana/gpu_app_runner/README.md)

## Работа со Spark

- [Работа со Spark](./docs/spark.doc.md)

## Работа со PyTorch

- [Работа с PyTorch](./docs/torch.doc.md)
