# Доставка кастомной статики

* Флаг `push_static`;
* Значение - строковое представление этого json'a:
```json
{
    "js": "alert(\"Hello\")",
    "js_urls": ["https://my.custom/js/file.js", "https://my.another.custom/js/file.js"],

    "css": "*{ background: black !important }",
    "css_urls": ["https://my.custom/css/file.css", "https://my.another.custom/css/file.css"]
}
```
## Создание test-id
Для вставки js/css кода в json test-id'а нужно сделать сначала отдельно json escape всего кода (через любой онлайн json escape сайт)
```plain
alert("Hello") -> alert(\"Hello\")
```
Затем вставить в json и сделать еще один json escape уже всего вместе.

```plain
{\n    \"js\": \"alert(\\\"Hello\\\")\",\n    \"js_urls\": [\"https://my.custom/js/file.js\", \"https://my.another.custom/js/file.js\"],\n\n    \"css\": \"*{ background: black !important }\",\n    \"css_urls\": [\"https://my.custom/js/file.css\", \"https://my.another.custom/js/file.css\"]\n}
```
### Escape в JS'e через stringify
Можно в консоли браузера сделать вот так через строку:
```js
JSON.stringify(`{
    "js": ${JSON.stringify(script.textContent)},
    "js_urls": ["https://my.custom/js/file.js", "https://my.another.custom/js/file.js"],

    "css": ${JSON.stringify(style.textContent)},
    "css_urls": ["https://my.custom/js/file.css", "https://my.another.custom/js/file.css"]
}`)
```
Или так через JS Object:
```js
JSON.stringify(JSON.stringify({
    js: script.textContent,
    js_urls: ["https://my.custom/js/file.js", "https://my.another.custom/js/file.js"],

    css: style.textContent,
    css_urls: ["https://my.custom/js/file.css", "https://my.another.custom/js/file.css"]
}));
```

### Пример test-id
```json
[
  {
    "HANDLER": "WEB",
    "CONTEXT": {
      "MAIN": {
        "REPORT": {
          "csp_disable": "1",
          "push_static": "{\n    \"js\": \"alert(\\\"Hello\\\")\",\n    \"js_urls\": [\"https://my.custom/js/file.js\", \"https://my.another.custom/js/file.js\"],\n\n    \"css\": \"*{ background: black !important }\",\n    \"css_urls\": [\"https://my.custom/js/file.css\", \"https://my.another.custom/js/file.css\"]\n}"
        }
      }
    },
    "TESTID": [
      "371381"
    ],
    "CONDITION": "project:web && !handler:YxWeb::MiscHandlers::AppHostExternal::chat",
    "RESTRICTIONS": [
      {
        "services": "blogs,people,profile,searchapp,turbo,web"
      }
    ]
  }
]
```
## На странице
* Сначала вставляются ссылки, затем инлайн элемент;
* Полноценно работает только через test-id.
* Каждый элемент снабжается id,
    * для инлайн `push-static_{js|css}_inline`,
    * для ссылок `push-static_{js|css}_url{индекс_ссылки}`
* Для вставки ссылок рекомендуется отключить СSP через флаг `csp_disable=1`