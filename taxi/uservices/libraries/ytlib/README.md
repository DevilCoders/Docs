# Библиотека для работы с Yt

## Подготовка окружения

### Установка дополнительных пакетов

Для сборки потребуется свежая версия пакета yt-wrapper:

- ubuntu:
`sudo bash -c 'apt-get update && apt-get install libyandex-taxi-yt-wrapper-dev'`
- mac:  `brew update && brew install yt-wrapper`

### Получение токена

Для работы с yt потребуется токен. Свой персональный токен можно узнать на
https://oauth.yt.yandex.net/.

Если по какой-то причине нужно пользоваться продакшеновским секретом, коллеги
наверняка подскажут, нужный раздел [секретницы](https://yav.yandex-team.ru/).

### Передача токена при локальной разработки

При локальной разработке не рекомендуется прописывать секреты в файлы,
находящиеся под управлением системы контроля версий, чтобы случайно не
закоммитить чувствительную информацию в общедоступный репозиторий.

Чтобы избежать такой проблемы, следует задать токен через переменную окружения
`YANDEX_TAXI_YTLIB_TOKEN` в консоли, из которой запускается сервис.

- bash/zsh: `export YANDEX_TAXI_YTLIB_TOKEN=your-secret-token`
- IDE: ищи что-то похожее на «environment variables» в настройках


## Подготовка сервиса для использования Yt
### service.yaml

В service.yaml нужно будет добавить:

1. Зависимость от библиотеки ytlib в секцию libraries:
```
libraries:
  - yandex-taxi-library-ytlib
```

2. Заглушку для значения токена — это необходимо, чтобы сервис парсил локальную
конфигурацию:
```
secdist:
  testsuite:
    values:
      YT_CONFIG:
        token: "placeholder"
```
3. В `config_vars` (`services/$SERVICE/config/config_vars.user.default.yaml`)
задаем дефолтный размер пула потоков для работы с yt:
```
yt_worker_threads: 8
```
Размер этого пула определяет, сколько yt операций могут выполняться одновременно.

## Использование компонента в коде сервиса
1. Добавляем ссылку на компонент в структуру `Extra`:
```
// src/custom/dependencies.hpp
#include <ytlib/ytlib_component.hpp>

namespace custom {
class Dependencies {
  struct Extra {
    ytlib::component::YtLib& ytlib;
  };
};
}
```
2. Получаем компонент в конструкторе:
```
// src/custom/dependencies.cpp
// Dependencies::Dependencies(const components::ComponentConfig& /*config*/,
//                           const components::ComponentContext& context)
    : ytlib_(context.FindComponent<ytlib::component::YtLib>())
```

