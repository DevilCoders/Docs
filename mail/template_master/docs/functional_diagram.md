Template master состоит из следующих основных модулей:

* Database module
* WebServer
* Router module
* TemplatePool module
* TemplateMaster module

## Database module
<details><summary><b>Possible interface:</b></summary><p>

```cpp
class IDatabase : public yplatform::module {
public:
    virtual TExpected<TStableTemplates> FindSimilarTemplates(
            NTemplateMaster::TContextPtr context,
            const TTemplateSign& hashes,
            int32_t limit,
            TYield) noexcept = 0;

    virtual TExpected<TOptional<TStringStableTemplatePtr>> FindTemplateByStableSign(
            NTemplateMaster::TContextPtr,
            TTemplateStableSign,
            TYield) noexcept = 0;

    virtual TExpected<void> SaveTemplate(
            NTemplateMaster::TContextPtr,
            TStringStableTemplatePtr,
            TYield) noexcept = 0;

    virtual void AsyncSaveTemplate(
            NTemplateMaster::TContextPtr,
            TStringStableTemplatePtr,
            std::function<void(TExpected<void>)>) = 0;

    virtual ~IDatabase() = default;
};
```

</p></details>
<details><summary><b>Possible data structure:</b></summary><p>

```sql
CREATE TABLE sherlock.template_bodies (
    stable_sign bigint primary key,
    sign integer[],
    chunks jsonb
);
```

</p></details>

Модуль для работы с базой инкапсулирует логику работы с базой, и предоставляет следующее множество операций:

* Поиск шаблонов, которые похожи по наполнение на текущее сообщение
* Поиск шаблона по **stable sign**
* Удаление шаблона по **stable sign**
* Сохранения нового сваренного шаблона
* Сохранение и обновление статистики по шаблонам

## WebServer
Используется для приема http запросов

## Router module
Основные задачи модуля

* Получение и обновление списка хостов из Qloud Api
* Отправка и получение ответа от другого инстанса template master'a


## TemplatePool module
Основные задачи модуля

* Хранение еще не готовых шаблонов
* Нечеткий поиск похожих шаблонов используя алгоритм [MinHash](https://medium.com/engineering-brainly/locality-sensitive-hashing-explained-304eb39291e4)
* Вычисление [LCS](https://en.wikipedia.org/wiki/Longest_common_subsequence_problem) с похожими шаблонами и выбор 
шаблона для обновления 
* Обновление шаблона при матче с письмом
* Сохранение готовых шаблонов в базе


####  Как происходит добавление TMessage в TemplatePool
![](imgs/template_pool.jpg)


## TemplateMaster Module

* Извлечение факторов из письма
* Определение хоста для роутинга письма исходя из извлеченных факторов
* Токенизация письма и создание объекта TMessage

P.S На данный момент используется рандомный выбор инстанса, в качестве потенциального улучшения можно использовать 
алгоритм [SimHash](http://matpalm.com/resemblance/simhash/)
