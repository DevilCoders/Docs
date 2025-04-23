## ymod_metricserver

### Что это?
Модуль платформы, который собирает метрики со всех прочих модулей и отдает их по HTTP в унифицированном текстовом формате.
Позволяет абстрагировать код от конкретной системы мониторинга и легко адаптировать под новые системы.

### Виды метрик
Метрики бывают трех видов:
- numeric: целое или вещественное число  
  Например: 42
- raw_hgram: список чисел  
  Например: [1,3,1,1,1]
- bucket_hgram: список взвешенных интервалов, задаваемых парами чисел (левая граница, вес).  
  Например: [[1,100],[3,300],[5,500]]  
  Интервал [1, 3) имеет вес 100; интервал [3, 5) имеет вес 300; интервал [5, ∞) имеет вес 500.  

### Пример использования
```C++
struct test_module: yplatform::module
{
    ptree get_stats()
    {
        ptree stats;
        stats.put_value("numeric", "42");
        return stats;
    }
};
```

```
$ curl -s localhost:8092/metrics
numeric 42
```

### Пример конфигурации
```
-   _name: metrics
    system:
        name: metrics
        factory: ymod_metricserver::impl
    configuration:
        port: 8092 # в целях унификации рекомендуем оставлять порт 8092
        reactor: metrics
```

### Названия метрик
Сгенерированные названия метрик, возращаемые metricserver, удоволетворяют следующим правилам:
- Название метрики состоит из alnum символов и некоторых специальных символов: '-', '.', '_'
- Название метрики начинается и заканчивается на alnum символы и не содержит 2 и более специальных символов подряд.
- Метрики гистограмм завершаются на '_hgram'

### Описание текстового формата в BNF
```
metric := numeric_metric | hgram_metric;
numeric_metric := numeric_metric_name, " ", numeric_value;
hgram_metric := hgram_metric_name, " ", ( raw_hgram | bucket_hgram );

raw_hgram := "[", numeric_value, { ",", numeric_value }, "]";
bucket_hgram := "[", bucket, { ",", bucket }, "]";
bucket := "[", numeric_value, ",", numeric_value, "]";
numeric_value := uint | double;

hgram_metric_name := numeric_metric_name, "_hgram";
numeric_metric_name := alnum_symbol, { alnum_symbol }, { special_symbol, alnum_symbol, { alnum_symbol } };

special_symbol := "." | "_" | "-";
alnum_symbol := lowercase_letter | digit;
```

### Как получить метрики гистограмм
``` C++
ptree make_raw_hgram(const vector<string>& values)
{
    ptree hgram;
    for (auto&& value : values)
    {
        ptree ptree_value;
        ptree_value.put("", value);
        hgram.push_back(make_pair("", ptree_value));
    }
    return hgram;
}

ptree make_bucket_hgram(const vector<pair<string, string>>& buckets)
{
    ptree hgram;
    for (auto&& bucket : buckets)
    {
        ptree ptree_bucket;
        ptree border;
        border.put("", bucket.first);
        ptree_bucket.push_back(make_pair("", border));

        ptree weigth;
        weigth.put("", bucket.second);
        ptree_bucket.push_back(make_pair("", weigth));

        hgram.push_back(make_pair("", ptree_bucket));
    }
    return hgram;
}

struct test_module: yplatform::module
{
    ptree get_stats()
    {
        ptree stats;

        stats.add_child("raw_hgram", make_raw_hgram(std::vector<string>{ "1", "2", "3" }));

        vector<pair<string, string>> bucket_hgram;
        bucket_hgram.emplace_back("1", "1");
        bucket_hgram.emplace_back("2", "2");
        bucket_hgram.emplace_back("3", "3");
        stats.add_child("bucket_hgram", make_bucket_hgram(bucket_hgram));

        return stats;
    }
};
```

```
$ curl -s localhost:8092/metrics
raw_hgram [1,2,3]
bucket_hgram [[1,1],[2,2],[3,3]]
```
