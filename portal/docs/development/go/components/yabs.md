# Компонента `yabs`

Хранит обработанные флаги таргетинга, полученные из ответа в Баннерокрутилку (БК) по адресу `yabs.yandex.ru`.
Отсюда аббревиатура BK в имени поля `BKFlags`.

В Morda Perl обработка ответа и парсинг происходит в модуле [MordaX::Banners](https://a.yandex-team.ru/arcadia/portal/main/lib/MordaX/Banners.pm).

## Кипер {#keeper}
[a.yandex-team.ru/portal/avocado/libs/utils/yabs](https://a.yandex-team.ru/arc_vcs/portal/avocado/libs/utils/yabs)

Интерфейс [`contexts.Base`](https://a.yandex-team.ru/arcadia/portal/avocado/morda-go/pkg/contexts/base.go) предоставляет методы:

* `GetYabs() models.Yabs` – возвращает модель или пустую структуру с последующим выводом предупреждения в лог и в Error Booster в случае
  отсутствия данных
* `GetYabsOrErr() (models.Yabs, error)` – позволяет проверить наличие модели без логирования предупреждения

В Apphost'е данные Yabs'а передаются в отдельном протоайтеме `yabs_context`.  Для использования данных Yabs в хэндлере
Morda Go необходимо добавить соответствующую зависимость на ребро из узла `GO_SELECTOR` в узел, вызывающий ваш хэндлер.

## Модель {#model}
[a.yandex-team.ru/portal/avocado/libs/utils/base/models](https://a.yandex-team.ru/arc_vcs/portal/avocado/libs/utils/base/models/yabs.go)

```go
type Yabs struct {
    BKFlags map[string]BKFlag // отображение "имя БK-флага" -> "ссылки для открутки счётчиков"
}
```

```go
type BKFlag struct {
    ClickURL string // 
    CloseURL string
    LinkNext string
}
```

### Методы {#methods}
* Для получения или проверки существования флага используйте стандартный механизм проверки в словарях Go:
```go
yabsData := ctx.GetYabs()
if flag, ok := yabsData.BKFlags["some_useful_flag"]; ok {
    _ = flag.ClickURL
    // your code here...
}
```
* `GetOrderedBkFlags() []string` – возвращает отсортированный список всех имеющихся БК-флагов. Используется только
в сравнивалке компонент в узле `GO_SELECTOR`
