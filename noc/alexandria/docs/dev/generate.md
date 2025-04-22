## Кодогенерация

Тезисное описание генератора:
* Matchers и Softs определены в yaml-файлах​
* Файлы помещены в Embed FS​
* При сборке (ya make) запускается Generator на основе text/tamplate​
* Результатом генерации является набор методов для сборки и декларации Stash
* Полученный genstash с помощью InitStash() используется для создания Stash-интерфейса Александрии
* Генерация делает базовую проверку ввода
* Стандартный Arcadia Autocheck CI запускает тесты консистентности (или ya make –t)
 

### Особенности ya.make
`noc/alexandria/stash/generator` это отдельный GO_PROGRAM,  
[generator ya.make](https://a.yandex-team.ru/arc/trunk/arcadia/noc/alexandria/stash/generator/ya.make):
* Генератор собирается и запускается благодаря макросу RUN_PROGRAM в `noc/alexandria/stash/genstash`
* Все yaml-файлы являются частью сборки, благодаря макросу GO_EMBED_PATTERN