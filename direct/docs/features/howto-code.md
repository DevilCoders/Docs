[Концепции, договоренности, ведение фичи в трекере](concept.md) <br/>
# Добавление фичей { #add }


## 1. Добавьте фичу в конфиг { #modify-feature-config }

{% note tip %}

Выберите такое название, которое не будет совпадать с именами других сущностей (и не будет их подстрокой). Например, при запуске нового типа баннера не стоит называть фичу так же, как новый тип, так как при удалении фичи будет сложно найти её вхождения при помощи поиска по репозиторию. [Пример с фичей 'cpm_indoor'](https://a.yandex-team.ru/search?search=cpm_indoor,%5Edirect.*,jCi,arcadia,,500&repo=arc).

{% endnote %}

{% note tip %}

Если в pull request при добавлении фичи без изменения фронтового кода падают фронтовые проверки, скорее всего что-то сломалось в самой проверке и можно отжать галочки

{% endnote %}

### Ручное добавление

Добавьте фичу в конец файла [feature.yaml](https://a.yandex-team.ru/arc_vcs/direct/libs-internal/base-model/src/main/resources/feature.yaml):
```yaml
reasons_filter_links_in_status_popup: #ключ фичи
  text: Описание # обязательный ключ, текстовое описание
  type: permanent # опциональный ключ, тип фичи, по умолчанию temp, см FeatureType
  status: deprecated # опциональный ключ, добавляет аннотацию `@Deprecated`. Предлагается ставить для фичей, которые включены на 100% и можно выпиливать
```
- Ключ фичи укажите в нижнем регистре.
- `text:` укажите описание фичи для интерфейса.
- `type:` укажите тип фичи в нижнем регистре если нужна не TEMP фича. [FeatureType](https://a.yandex-team.ru/arc/trunk/arcadia/direct/libs-internal/base-model/src/main/java/ru/yandex/direct/feature/FeatureType.java) ([подробнее о типе](concept.md#temp_permanent)).
- `status: deprecated` при добавлении не нужен
- Выполните в папке `arcadia/direct` команду `./bin/generate_features.sh`, появятся изменения в [FeatureName](https://a.yandex-team.ru/arc/trunk/arcadia/direct/libs-internal/base-model/src/main/java/ru/yandex/direct/feature/FeatureName.java) и [features](https://a.yandex-team.ru/arc/trunk/arcadia/adv/frontend/services/dna/src/typings/features.ts)
- Создайте ревью и закоммитьте в trunk изменения. Если в pr только создается фича через скрипт, достаточно одного ок'а от любого разработчика
- Для фронтендеров: важно [правильно расставлять](../concepts/dev/ticket-workflow.md#affected-apps) значение web в поля affected_apps/tested_apps для задачи, в рамках которой фича добавляется.

см так же [README.md](https://a.yandex-team.ru/arc_vcs/direct/libs-internal/feature-generator/README.md)

### Автоматическое добавление через sandbox таску

Sandbox задача для добавления фичей — DIRECT_FEATURE_UPDATE.

[Пример](https://sandbox.yandex-team.ru/task/1222335317/view) выполнения sandbox таски.

Как пользоваться:
- Создать задачу в st.yandex-team.ru (или склонировать существующую)
- Заполнить поля с тикетом, названием фичи, описанием в sandbox таске
- Запустить — будет создано ревью с добавлением фичи
- Если включена галочка Commit without review, то ревью смержится задачей, без код-ревью и ожидания прохождения тестов

Если ревью не получилось смержить из-за конфликтов, достаточно запустить задачу еще раз — будет сгенерировано ревью от свежего транка.
Пока поддерживается добавление только 1ой фичи за раз.


## 2. Добавьте фичу в базу { #add-db }

{% note info %}

Чтобы фичу можно было добавить в базу из внутреннего инструмента ([prod](https://direct.yandex.ru/internal_tools/#add_features) | [testing](https://test-direct.yandex.ru/internal_tools/#add_features) | [devtest - 8998](https://8998.beta1.direct.yandex.ru/internal_tools/#add_features)), код фичи, добавленный в [пункте 1](#java-code), должен быть задеплоен в приложении java-web в соответствующее окружение. На бете `8998` фича появится при обновлении общей беты java-web во время выкладки релиза java-web. Если фича в базе нужна раньше, соберите собственную бету java-web из транка, и на ней воспользуйтесь внутренним инструментом.

{% endnote %}

Перейдите на страницу добавления фичи в целевом окружении ([prod](https://direct.yandex.ru/internal_tools/#add_features) | [testing](https://test-direct.yandex.ru/internal_tools/#add_features) | [devtest - 8998](https://8998.beta1.direct.yandex.ru/internal_tools/#add_features)):
- Укажите ключ фичи [feature.yaml](https://a.yandex-team.ru/arc_vcs/direct/libs-internal/base-model/src/main/resources/feature.yaml).
- Укажите ответственного за фичу [подробнее](concept.md#responsible). По умолчанию это **должен быть человек, ответственный за проект**, в рамках которого добавляется фича. На него автоматически будет назначен тикет, соответствующий фиче. О тикете читайте ниже.
- Укажите список наблюдателей - людей, которым может быть полезно наблюдать за изменением состояния фичи. Они автоматически будут добавлены в тикет в качестве фолловеров.
- Если фича при выдаче агентству должна включаться всем его клиентам - установите галочку "Фича для всех клиентов агентств".

{% note info "Тикет на фичу" %}

При создании фичи в базе автоматически создается тикет с ответственным и наблюдателями. В нем автоматика отражает изменения настроек фичи и включение/выключение для клиентов. Так же добавляются подсказки и напоминания о необходимых ручных действиях вроде включения фичи на ТС и удаления фичи из кода.

{% endnote %}

# Использование фичей { #usage }

## Как проверить фичу в окружении devtest { #usage-check-devtest }

- На странице [Управление доступом к фичам клиентов по логину (devtest - 8998)](https://8998.beta1.direct.yandex.ru/internal_tools/#switch_feature_for_client_by_login) во внутренних инструментах переключаем состояние фичи клиенту или оператору.
- Смотрим наличие либо отсутствие фичи в ответе [запроса](https://8998.beta1.direct.yandex.ru/web-api/grid/?#query%20%7B%0A%20%20client(searchBy%3A%20%7B%20login%3A%20%22yuber%22%20%7D)%20%7B%0A%20%20%20%20features%20%7B%0A%20%20%20%20%20%20availableClientCoreFeatures%20%7B%0A%20%20%20%20%20%20%20%20featureName%0A%20%20%20%20%20%20%20%20description%0A%20%20%20%20%20%20%7D%0A%20%20%20%20%7D%0A%20%20%7D%0A%20%20operator%7B%0A%20%20%20%20features%20%7B%0A%20%20%20%20%20%20availableOperatorCoreFeatures%20%7B%0A%20%20%20%20%20%20%20%20featureName%0A%20%20%20%20%20%20%20%20description%0A%20%20%20%20%20%20%7D%0A%20%20%20%20%7D%0A%20%20%7D%0A%7D%0A), в соответствующем поле.

## Как использовать фичу в Java { #usage-java }

Для проверки включенности фичей у клиента используйте [FeatureService](https://a.yandex-team.ru/arc/trunk/arcadia/direct/core/src/main/java/ru/yandex/direct/core/entity/feature/service/FeatureService.java).

{% note warning "Проверяйте включенность фичей только через enum FeatureName" %}

Использование фичей с помощью строковых констант, оторванных от основного enum `FeatureName` несёт опасность и неудобства: это усложняет поиск использований фичи в коде, и, как следствие, при удалении фичи из базы можно пропустить подобные места и разломать функциональность (подробнее об удалении из базы в [{#T}](#delete-db)).

{% endnote %}

## Как использовать фичу на фронте { #usage-front }

В dna схема получения фичей такая:
 - фичи на клиента получаем из [availableClientCoreFeatures](https://8998.beta1.direct.yandex.ru/web-api/grid/?#query%20%7B%0A%20%20client(searchBy%3A%20%7B%20login%3A%20%22yuber%22%20%7D)%20%7B%0A%20%20%20%20features%20%7B%0A%20%20%20%20%20%20availableClientCoreFeatures%20%7B%0A%20%20%20%20%20%20%20%20featureName%0A%20%20%20%20%20%20%7D%0A%20%20%20%20%7D%0A%20%20%7D%0A%7D%0A)
 - фичи на оператора получаем из [availableOperatorCoreFeatures](https://8998.beta1.direct.yandex.ru/web-api/grid/?#query%20%7B%0A%20%20operator%7B%0A%20%20%20%20features%7B%0A%20%20%20%20%20%20availableOperatorCoreFeatures%20%7B%0A%20%20%20%20%20%20%20%20featureName%0A%20%20%20%20%20%20%7D%0A%20%20%20%20%7D%0A%20%20%7D%0A%7D%0A)

В эти массивы приходят все доступные клиенту и оператору фичи, в виде значений enum'а `FeatureName`. На фронте эти поля преобразуются в два Set'а: `clientFeaturesSet` и `operatorFeaturesSet` и доступны в `commonData`. Включенность фичи проверяем через `.has(FeatureName.FEATURE_KEY)`. Таким образом, логика про то на ком проверять фичу, на клиенте или на операторе, переходит на фронтенд.

{% note warning "Проверяйте включенность фичей только через enum FeatureName" %}

Использование фичей с помощью строковых констант, оторванных от основного enum `FeatureName` несёт опасность и неудобства: это усложняет поиск использований фичи в коде, и, как следствие, при удалении фичи из базы можно пропустить подобные места и разломать функциональность (подробнее об удалении из базы в [{#T}](#delete-db)).

{% endnote %}

# Удаление фичей { #delete }

После того как фича включена на 100% в продакшене (для всех пользователей), её требуется удалить из кода, так как наличие в коде лишних ветвлений приводит к дополнительной сложности в разработке и поддержке.

{% note info "Ресурсы и сроки удаления фичи" %}

За выделение ресурсов для удаления фичи по умолчанию отвечает ответственный за проект, в рамках которого добавляется фича. На удаление фичи отводится срок в один месяц с момента включения на 100% в продакшене (подробнее в разделе [{#T}](concept.md#responsible)).

{% endnote %}

## 1. Удалите фичу из кода { #delete-code }

{% note warning "Фича должна быть включена у всех клиентов" %}

Прежде чем удалять фичу из [feature.yaml](https://a.yandex-team.ru/arc_vcs/direct/libs-internal/base-model/src/main/resources/feature.yaml), убедитесь, что она включена на 100% в продакшене ([Список фич](https://direct.yandex.ru/internal_tools/#get_features)), а так же что она не выключена принудительно у конкретных клиентов ([Список клиентов с доступом к фиче](https://direct.yandex.ru/internal_tools/#get_clients_for_features)). Проследите, что [ответственный](concept.md#responsible) за фичу знает, когда вы планируете её удалять, и никто не планирует её снова выключать. Подпишитесь на основной тикет, тогда в случае изменений настроек фичи вы об этом узнаете (подробнее о тикете в разделе [{#T}](concept.md#tracker)).

{% endnote %}

Прежде чем удалить фичу [feature.yaml](https://a.yandex-team.ru/arc_vcs/direct/libs-internal/base-model/src/main/resources/feature.yaml), убедитесь, что она не используется в коде фронтенда и бекэнда (не считая сгенерированных тайпингов в директории `dna/src/typings/`, `uac/src/schema/` и `direct-modules/src/shared/api/grid/generatedTypes.ts`).

Воспользуйтесь поиском по [директории direct/ в аркадии](https://a.yandex-team.ru/search?search=,%5Edirect%2F.*,ji,arcadia,,500&repo=arc), используя значения из enum. Если вы правильно указали фичу в поиске, то вы найдете её в `dna/src/typings/` или `uac/src/schema/` или `direct-modules/src/shared/api/grid/generatedTypes.ts`. Если не нашли, значит неправильно указали имя.

Воспользуйтель поиском по [проекту конструктора турболендингов](https://gitlab.yandex-team.ru/lp-constructor/constructor/), используя значения из enum. Поиск не должен вернуть вхождения строки.

## 2. Удалите фичу из базы { #delete-db }

{% note warning "Фича не должна использоваться в коде" %}

Удаление фичи из базы приведет к тому, что она "выключится". Если в момент удаления от неё всё ещё зависит условная логика, то она станет работать так, будто фичу выключили. Именно поэтому во внутреннем инструменте удаления фичи есть валидация, что enum в коде отсутствует. К сожалению, этой валидации недостаточно, так как фичи иногда проверяются по строке, заданной в виде отдельной константы (антипаттерн, но, к примеру, в Perl по-другому никак). Поэтому, очень важно проверить отсутствие фичи во всех кодовых базах в нижнем и верхнем регистрах (Perl, Java, фронтенд).

{% endnote %}

{% note warning "Удаление фичи из базы на своей бете" %}

Если планируете удалить фичу из базы на своей бете, то стоит учесть, что фича может использоваться как проверка с доступом к какому-то функционалу в java-приложении и после удаления фичи из базы - доступ к функционалу пропадет на общих java-инстансах. В таких случаях лучше удалить фичу из базы после сборки релиза и обновления java-инстанса.

{% endnote %}

Перейдите на страницу удаления фичей во внутренних инструментах ([prod](https://direct.yandex.ru/internal_tools/#view_or_delete_features) | [testing](https://test-direct.yandex.ru/internal_tools/#view_or_delete_features) | [devtest - 8998](https://8998.beta1.direct.yandex.ru/internal_tools/#view_or_delete_features)), выберите действие "Удалить одну фичу" и укажите значение фичи из enum.
