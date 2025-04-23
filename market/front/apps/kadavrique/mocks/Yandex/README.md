# Yandex

## searchWizardsJson (/search/wizardsjson)

Ручка получения индексов 

Сейчас поддерживаются параметры:
- type
- geo
- text

Данные в стейте хранятся в виде:

```
{
    Yandex: {
        searchWizards: [
            entity1,
            entity2,
        ]
    }
}
```

Каждая сущность должна иметь поле `filterForKadavr`, по которому сущности будут фильтроваться для ответа. Из самого ответа это поле удаляется

Пример:
```
entity1 = {
    ...
    filterForKadavr: {
        type: 'postal_codes',
        geo: 213,
        text: 'Москва, улица Льва Толстого, 16'
    }
};
entity2 = {
    ...
    filterForKadavr: {
        type: 'postal_codes',
        geo: 65,
        text: 'Новосибирск, улица Красноярская, 35'
    }
};
```

По запросу `https://yandex.ru/search/wizardsjson?text=Москва, улица Льва Толстого, 16&geo=213&type=postal_codes` будет отдаваться `entity1`,
по запросу `https://yandex.ru/search/wizardsjson?text=Новосибирск, улица Красноярская, 35&geo=65&type=postal_codes` будет отдаваться `entity2`.
