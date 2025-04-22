## Landlord
Сервис-владелец данных для автосгенерированных лендингов.

#### Testing
api: http://landlord.tst.geosmb.maps.yandex.net
tvm: 2024465

#### Production
api: http://landlord.geosmb.maps.yandex.net
tvm: 2024467

#### Полезные ссылки
* [ABC](https://abc.yandex-team.ru/services/maps-adv-clients-landlord/)
* Yav [testing](https://yav.yandex-team.ru/secret/sec-01enwmyc62etmabqkhyqc3b7h2) [production](https://yav.yandex-team.ru/secret/sec-01eppk4m5jscs1v2ayq45he8jw)
* [CD](https://a.yandex-team.ru/ci/maps-adv-clients-landlord/releases/timeline?dir=maps_adv%2Fgeosmb%2Flandlord%2Fserver&id=stable-release)
* [Sandbox resources](https://sandbox.yandex-team.ru/resources?type=GEOSMB_LANDLORD)
* [Deploy](https://deploy.yandex-team.ru/projects/geosmb-landlord)
* Awacs [testing](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/landlord.tst.geosmb.slb.maps.yandex.net/show/) [production](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/landlord.geosmb.slb.maps.yandex.net/show/)
* YC [PostgreSQL](https://yc.yandex-team.ru/folders/akus6cjpv20pcuhisjqc)
* Solomon [админка](https://solomon.yandex-team.ru/admin/projects/maps-adv-clients)


## API
Протоколы живут в `./proto/`.

#### Получение данных для лендинга по slug

`POST /external/fetch_landing_data/`

input: **organization_details.OrganizationDetailsInput**

output:
* **HTTP 200, organization_details.OrganizationDetails** - данные для лендинга
* **HTTP 401** - неправильный токен
* **HTTP 404** - опубликованных данных для переданного slug нет

#### Генерация начальный данных для biz_id

`POST /v1/generate_landing_data/`

input: **generate.GenerateDataInput**

output:
* **HTTP 201, generate.GenerateDataOutput** - данные успешно сгенерированы
* **HTTP 400, Error(code=VALIDATION_ERROR)** - ошибка валидации входных данных
* **HTTP 400, Error(code=NO_ORGS_FOR_BIZ_ID)** - для biz_id не найдено организаций
* **HTTP 400, Error(code=NO_ORGINFO)** - для удалось получить данные для организации, связанной c biz_id
* **HTTP 400, Error(code=BIZ_ID_ALREADY_HAS_DATA)** - biz_id уже имеет данные


#### Проверка свободности домена

`POST /v1/check_slug_is_free/`

input: **internal.landing_details.CheckSlugAvailableInput**

output: **HTTP 200, internal.landing_details.CheckSlugAvailableOutput**


#### Изменение домена

`POST /v1/update_slug/`

input: **internal.landing_details.UpdateSlugInput**

output: 
* **HTTP 204** - slug изменён
* **HTTP 400, common.Error(code=BIZ_ID_UNKNOWN)** - biz_id не найден
* **HTTP 400, common.Error(code=SLUG_IN_USE)** - slug занят


#### Изменения статуса опубликованности лендинга

`POST /v1/set_landing_publicity/`

input: **internal.landing_details.SetLandingPublicityInput**

output: 
* **HTTP 204** - статус изменён
* **HTTP 400, common.Error(code=BIZ_ID_UNKNOWN)** - biz_id не найден
* **HTTP 400, common.Error(code=NO_STABLE_VERSION_FOR_PUBLISHING)** - нет версии для публикации



#### Получение данных лендинга

`POST /v1/show_landing_details/`

input: **internal.landing_details.ShowLandingDetailsInput**

output:
* **HTTP 200, internal.landing_details.ShowLandingDetailsOutput** - данные лендинга
* **HTTP 400, common.Error(code=BIZ_ID_UNKNOWN)** - biz_id не найден
* **HTTP 400, common.Error(code=VERSION_DOES_NOT_EXIST)** - у biz_id не запрошенной версии


#### Редактирование данных лендинга

`POST /v1/edit_landing_details/`

input: **internal.landing_details.EditLandingDetailsInput**

output:
* **HTTP 200, internal.landing_details.EditLandingDetailsOutput** - новые данные лендинга
* **HTTP 400, common.Error(code=BIZ_ID_UNKNOWN)** - biz_id не найден


#### Получение вариантов для заполнения поля категорий

`POST /v1/suggests/categories/`

input: **internal.suggests.SuggestInput**

output:
* **HTTP 200, internal.suggests.PlainSuggest** - новые данные лендинга
* **HTTP 400, common.Error(code=BIZ_ID_UNKNOWN)** - biz_id не найден


#### Получение вариантов для заполнения поля ключевых особенностей

`POST /v1/suggests/plain_extras/`

input: **internal.suggests.SuggestInput**

output:
* **HTTP 200, internal.suggests.PlainSuggest** - новые данные лендинга
* **HTTP 400, common.Error(code=BIZ_ID_UNKNOWN)** - biz_id не найден


#### Получение вариантов CTA-кнопки

`POST /v1/suggests/cta_button/`

input: **internal.suggests.SuggestInput**

output:
* **HTTP 200, internal.suggests.CTAButtonSuggest** - доступные для выбора кнопки
* **HTTP 400, common.Error(code=BIZ_ID_UNKNOWN)** - biz_id не найден


#### Получение доступных цветов

`GET /v1/suggests/color_presets/`

output:
* **HTTP 200, internal.suggests.ColorPresetsSuggest** - доступные для выбора цвета


## Генерация данных для лендинга
При первой генерации данных для biz_id из BVM достаются пермалинки бизнеса, затем для
первого пермалинка запрашиваются данные в геопоиске. В БД сохраняются следующие данные (при их наличии):
 - название организации;
 - список категорий;
 - шаблон ссылки на логотип (ссылка вида https://avatars.mds.yandex.net/get-altay/1439437/2a0000016788e2c8424feb335b015e6cb0c5/%s,
 где %s - alias размера в Аватарнице, доступные alias-ы можно увидеть, например, [здесь](http://avatars-int.mds.yandex.net:13000/getimageinfo-altay/1439437/2a0000016788e2c8424feb335b015e6cb0c5));
 - пермалинк (если в геопоиск был передан пермалинк-дубликат, вернётся голова);
 - координаты;
 - форматированный адрес;
 - телефон;
 - ссылка на сайт;
 - ссылки на соцсети (vkontakte, facebook, instagram, twitter);
 - текстовые теги (например, "Оплата картой").

## Выдача данных для рендеринга лендинга
Из БД выдаются сохранённые данные с учётом настроек видимости блоков, выставленных
владельцем (по умолчанию все блоки отображаются).
Дополнительно налету получаются:
 - расписание работы организации из геопоиска;
 - список представляемых услуг из CRM-маркета.
