# get_url - способ скачать, распарсить и сохранить HTTP-ресурс

## Параметры

- `url` - HTTP URL до ресурса который будет скачиваться. Обязательное поле. Примеры:
  - `http://export.site.com/some_data`
  - `https://export.site.com/some_data.json`
  - `https://export.site.com/some_data.yaml`
- `parser` - Тип данных которые нужно распарсить. Опциональное. Возможные значения
  - `str`
  - `json`
  - `yaml`

## Определение парсера

Если параметр `parser` не указан он будет определяться автоматически в следующем порядке

1) По HTTP-заголовку `Content-Type`, например: `application/json`, `application/yaml`
2) По расширению файла в URL, например: `/data.json`, `/data.yaml`
3) Используем значение по-умолчанию - `str`

## Доступ к данным

Имя переменной в которой будет сохранен ресурс задается через общий параметр `register`:

```yaml
name: get-url-example
actions:
  - name: download some data
    get_url:
      url: http://example.com/some-data.json
    register: some_data_var
```

После этого к нему можно обратится из jinja-выражения:

```yaml
  # Используем some_data_var['param']
  - name: use for command from downloaded data
    execute: {cmd: [{cmd: "set some param {{ some_data_var['param'] }}" }]}
```

## Ограничения

Сохранить можно только текстовые данные.

Размер ресурса строго ограничен 100 KB. Это требуется поскольку данные сохряняются в общую базу и хранятся вместе с остальным контекстом джобы.
