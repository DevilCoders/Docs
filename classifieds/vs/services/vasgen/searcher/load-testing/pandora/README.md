## Нагрузочное тестирование `gRPC` сервиса

### Прежде чем начать

Рекомендуется прочитать:
1. https://wiki.yandex-team.ru/load/pandora/
2. https://github.com/YandexClassifieds/etc-mono/blob/master/services/spamalot/gun/README.md

## Введение

`Pandora` – генератор нагрузки, написанный на Go.
`Pandora` задумана как расширяемый инструмент: пользователи могут писать свои компоненты.
Это можно использовать для поддержки нестандартных протоколов (`protobuf`, `gRPC`).
Компоненты пишутся на `Go`, кастомный генератор собирается в бинарь непосредственно перед стрельбой.

## Создание кастомного компонента

1. Настроить окружение для работы с `Go`
2. Скомпилировать свои `gRPC` сервисы в `Go`:  
```protoc --go_out=. --go-grpc_out=. --go_opt=paths=source_relative --go-grpc_opt=paths=source_relative all.proto```  
Чтобы не разбираться с импортами можно положить все нужные протобафы в один файл.
3. Убедиться что в скомпилированном коде есть все нужные сообщения и `gRPC` сервисы.
4. Написать компонент (пример - `Main.go`, `go.mod`)
5. Создать файл с патронами (пример - `ammo.json`)

## Локальная стрельба
1. Создать конфиг для локальной стрельбы (пример - `load.yaml`)
2. Собрать и запустить компонент.

## Стрельба из яндекс.танка
1. Собрать компонент `env GOOS=linux GOARCH=amd64 go build`
2. Залить компонент и патроны в продовый `MDS` согласно [инструкции](https://wiki.yandex-team.ru/Load/LunaPark/dev/api/kshm/#zalivkapatronovvxranilishhemds).
3. Создать конфиг для `firestarter` (пример - `firestarter.yaml`). В конфиг вставить ссылки на пушку и патроны из п.2.
4. Залить свой конфиг в `https://lunapark.yandex-team.ru/firestarter/` и запустить стрельбу.

## Примеры стрельб
https://st.yandex-team.ru/VS-461  
https://nda.ya.ru/t/zS4Rh0Tc3boVbE

## Полезные ссылки
[telegram chat: Yandex Tank && Lunapark support](https://t.me/joinchat/BkIYdz-zGT40Ql-TxPZ04A)
