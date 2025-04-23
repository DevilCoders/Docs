# Наши porto-слои для Nirvana

## Общая информация о porto-слоях

Porto-слои в Nirvana это способ подготовить требуемое окружение для запуска Job-операции (ближайший аналог - слои в Docker).
Для сборки используется [интерфейс заведения словя в Nirvana](https://nirvana.yandex-team.ru/create-layer), где можно указать используемый родительский слой, настроить переменные окружения и выбрать скрипты, которые подготовят слой к работе.
После создания слоя будет запущен граф сборки, который можно будет увидеть во вкладке [Instances](https://nirvana.yandex-team.ru/instances). По окончанию сборки слой можно использовать.

## Использование porto-слоя в операциях

Для использования porto-слоя нужно:
- получить его ID на странице просмотра слоя (пример ID: `ddd3938f-3f55-484b-b314-d5e0d329e9d4`)
- на экране создания операции выбрать Job-процессор и добавить параметр `job-layer`
  - параметр должен быть списком строк
- после добавления параметра требуется добавить в него полученный ранее ID слоя
- готово, слой будет применен перед запуском операции

## Документация

Документацию по porto-слоям можно найти по слеующим ссылкам:
- [Актуальная документация в этушке](https://clubs.at.yandex-team.ru/nirvana/4614)
- [Устаревшая документация на wiki](https://wiki.yandex-team.ru/nirvana/manual/createoperation/volumes/)

## Наши porto-слои для Nirvana

### dcsaap-tvmtool

Позволяет использовать TVM в операции, так как содержит в себе установленный tvmtool:
```bash
bash -c '

export TVMTOOL_LOCAL_AUTHTOKEN="`openssl rand -hex 16`"
tvmtool add --secret "<tvm client secret>" --src "2017385:dcsaap-dev" --dst "2017385:dcsaap-dev" -c ./tvmtool.conf
tvmtool --port 18080 -c ./tvmtool.conf

curl -H "Authorization: $TVMTOOL_LOCAL_AUTHTOKEN" 'http://localhost:18080/tvm/tickets?dsts=2017385'
'
```

[Porto-слой в Nirvana](https://nirvana.yandex-team.ru/layer/d7640172-3fc6-47b4-a0b3-2450df5118bb)
