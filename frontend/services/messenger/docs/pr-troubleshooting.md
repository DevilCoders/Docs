# Если бета в PR не открывается

## Проверка работы production конфигурации локально

1. Собрать production бандл из папки с исходниками `npm run build`.
2. Запустить локальный Report Renderer:
```
  ~/.templar/ynode/bin/ynode
  ~/.templar/report-renderer/node_modules/luster/bin/luster.js
  ~/.templar/report-renderer/config.js --templates-package routes.json
```
3. Если RR сразу-же выключается (появляется `console prompt`), смотрим лог `logs/current-report-renderer_debug-9780`.
4. Если после запуска RR работает, пробуем отправить POST-запрос на адрес `localhost:9780/chat:phone` со следующим телом запроса:
```JSON
{
  "cgidata": {
    "hostname": "yandex.ru",
    "args": {}
  },
  "reqdata": {
    "experiments": {
      "slots": []
    },
    "reqid": "123123123",
    "ruid": "2384283478",
    "is_yandex_net": 1,
    "user_region": {
      "name": {
        "ru": {}
      }
    },
    "passport": {},
    "device_detect": {
      "OSFamily": "iOS",
      "device": "desktop"
    }
  }
}
```
5. Если в ответ получаем `200OK` и `html`, то всё работает. Если нет — опять смотрим лог `logs/current-report-renderer_debug-9780`.
