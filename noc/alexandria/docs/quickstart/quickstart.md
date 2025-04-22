## Преамбула
В данном разделе кратко разбираются основные шаги по взаимодействию с Александрией.

Предварительно рекомендуется ознакомиться с определениями:
- [Matcher/Матчер](../hld/match.md)
- [Soft/ПО](../hld/softs.md)
- [Recognizer/Признаватор](../hld/recognizers.md)

Также рекомендуется уделить внимание инструментам **devtools**
- [Быстрый старт](https://docs.yandex-team.ru/devtools/intro/quick-start-guide)
- [Манипуляции с arc](https://docs.yandex-team.ru/devtools/src/arc/workflow#workflow)   
- [Манипуляции с ya make](https://docs.yandex-team.ru/devtools/build/ya?searchQuery=ya%20make#ya-make)  

# Сценарии использования
## 1. Изменить желаемое ПО для группы устройств (для PNS/"рубёвой наливки" и сценариев ЦК)
### Известная платформа, новый желаемый релиз ПО:
_в т.ч. если поменялся патч или неосновной пакет._
* Добавить новый файл Soft [сюда](https://a.yandex-team.ru/arc/trunk/arcadia/noc/alexandria/stash/generator/source/soft) 
  * Cкопировав соседний похожий файл 
  * Или сгенерировав [с действующего устройства через API](https://alexandria.yandex-team.ru/swaggerui/#/Recognize/post_recognize_gen_)
* Изменить указатель SoftID в [Matchers](https://a.yandex-team.ru/arc/trunk/arcadia/noc/alexandria/stash/generator/source/matcher/matchers.yaml) на новый
  * Опционально: добавить старый SoftID в список Acceptable или Dangerous для этого матчера.
* Применить изменения согласно [разделу инструкции](../repository/contribute.md)

{% note info %}

Неправильно заменять один файл ПО другим или редактировать старый.  
Очень плохо менять содержимое файла ПО, оставляя ему прежнее имя.    
Создавать новые экземпляры ПО - это хорошо, это помогает признаваторам и отчёту.

{% endnote %}

### Новая платформа, с известным типом ПО(breed)
* Добавить новый файл Soft [сюда](https://a.yandex-team.ru/arc/trunk/arcadia/noc/alexandria/stash/generator/source/soft) 
  * Cкопировав соседний похожий файл, изменив имя и содержимое 
  * Или взяв [с устройства через API](https://alexandria.yandex-team.ru/swaggerui/#/Recognize/post_recognize_gen_)
* Создать новое правило в [Matchers](https://a.yandex-team.ru/arc/trunk/arcadia/noc/alexandria/stash/generator/source/matcher/matchers.yaml) 
* Применить изменения согласно [разделу инструкции](../repository/contribute.md)


### Новая платформа, новый тип ПО(breed)
[Завести тикет](https://st.yandex-team.ru/createTicket?queue=NOCDEV&_form=75230)

## 2. Выделить новую группу устройств в Matchers
* Вероятно у вас есть причина, согласно [этому разделу](../repository/recommendations.md). Новая модель устройств или новая роль для известной модели, это отличный повод.
* Не забывайте про First Match
* Применить изменения согласно [разделу инструкции](../repository/contribute.md)

## 3. Признаватор не справился с определением экземпляра ПО, но его важно контролировать
* Убедитесь, что этот тип ПО(breed) уже реализован в [признаваторах](https://a.yandex-team.ru/arc/trunk/arcadia/noc/alexandria/internal/usecases/recognizers)
* Убедитесь, что такой экземпляр ПО существует в [хранилище]((https://a.yandex-team.ru/arc/trunk/arcadia/noc/alexandria/stash/generator/source/soft)).
* Исправить недочёты или завести [тикет в NOCDEV](https://st.yandex-team.ru/createTicket?queue=NOCDEV&_form=72658)