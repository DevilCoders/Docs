# Рекламные ссылки на счетчики просмотров и переходов

В этом документе описывается принцип работы ссылок на счетчики просмотров и
переходов. А также то, как с этими ссылками должны взаимодействовать клиенты.

## ToC

1. [Какие бывают ссылки и зачем нужны](#what-and-why)
2. [Какие объекты сейчас могут быть "рекламными"](#advert-objects)
3. [Какие бывают проблемы с событиями/рекламными ссылками](#problems)
4. [Как нужно работать с ссылками клиентам](#client-behaviour)
	1. [Примеры](#client-behaviour-examples)
	2. [Про задержку в отправке событий](#client-behaviour-send-delay)
	3. [Какие параметры нужно передавать при продергивании
	   ссылок](#client-behaviour-send-params)
5. [Ссылки и источники](#links-and-sources)

<a id="what-and-why"></a>

## Какие бывают ссылки и зачем нужны

На данный момент в Еде существует два вида ссылок:

- ссылка на счетчик просмотров конкретного рекламного объявления (далее
  view_url)
- ссылка на счетчик переходов конкретного рекламного объявлени (далее
  click_url)

Переходом (или продергиванием) по ссылке называется действие, когда клиент
посылает HTTP GET запрос по ссылке соотвествующего вида.  
Все переходы по ссылкам мы называем событиями по аналогии с тем, как они
называются в баннерной крутилке.

Ссылки нужны для следующего:

- если объявление размещается по стратегии "средней цены за клик", то переход
  по click_url спишет деньги рекламодателя
- если объявление размещается по стратегии "средней цены за n показов", то
  переход по view_url спишет деньги рекламодателя
- учитывать в движке аукциона, сколько раз показали то или иное объявление,
  чтобы в дальнейшем правильно предсказывать CTR
- учитывать в движке аукциона, сколько раз кликнули по тому или иному
  объявлению, чтобы в дальнейшем правильно предсказывать CTR
- рекламодатель видит статистику просмотров/переходов по своим объявлениям в
  личном кабинете (в вендорке)

CURL с примером для view_url:

```
curl 'https://yabs.yandex.ru/count/WL0ejI_zO7u0DGe0n156BCNgpMyAZWK0VW4GWY0nQxjMOW00000uhFHsy0BjwAhq3F050Q06iAW1mGPMIWmaOuvJ0ycf1wJKjCXj-JuQi0U0W9WyyGTS7KIRpKd93j081AeB46_TQhcar000bV5GxOVS1G3m2mhW3OA0W42G4E60retbhVI3AlWG4AWHm8GzwHBpXhk_mbRzfF0I4DWLmOhsxAEFlFnZyA0MY9JQaWR95l0_WHUe5mcP6D0O4FWO-fweszJLkh9uW1c0wONvZypeZeW1a1a1i1dMbB6WiipZgGEu6V___m7I6H9vOM9pNtDbSdPbSYzoDZKoBJNe6O320_0PWC83c1hyy8W2i1jak1i5WXmDC651EZHnLMDLMLLPD-aSW1t_Vmm0KiWOF19oHBk6XabU2yc2n3WkMyOgnm5Iy92W9yyeEY1HFRArA7i0~1=WgWejI_zO0O2zHG0D2NAghSL1WC2S9I3qwEUeg7pom600PA__0A80P3ilO2C0P01ylQTWzc0W802c07ozfs3MRW1hDQkfIJO0RRtuAG1u06qzE2a0UW1s06W0e3yw1Q00zowaDe9Y0FDawLsc0F9n1AW0mIm0u7l0eW5_zfGa0Nndgu2i0N3mXIu1TFhJC05rEE_0SW5z-0mu0K5c0RMyAKAg0Qmg06m1u20c3ou1u05u0U62l47N1r4cyr9oGw020G8u0Y0lhGBw0d9243u2e2r6DaBfDIqo6tvFXhe2__QK8WCfARUlW6f351hTEI3lk8_w0oN0eaEmSgXHRRprQ0Em8Gz24204Dlvs2AWg801eH4qCpCpCpFZ6S3FrUTvJZ-n4h8EMpZDXkG_wHBpXhk_mbRzf9WJ2E0J-xsJ0Q0K-xsJ0QWKg8t41C0KWAAL4SWK1_RXiP86w1I40j0Lzk6naWRO5S6AzkoZZxpyOw0MY9JQaWR95W3mFz0MfARUlW615_0_c1U1kiukm1Uq5j0Nq8O3s1UWnJsP6A0O3B0OwTJQaWRu6FgUgDlKrRgoU80PWEc5-O_Cw8w80P0P0Q0PiAW1k1de6O320_0PWC83WHh__wTPWIXPn8WQm8Gzc1hyy8W2k1e6zHe10000WXiWCJPZDJSpCM4pPM9ZD3aqP3bcOs4rE3LbOs8uPMCsC36m6sIu6mNf6m00040M41X1y1lfqbxf780T_t-P7Q0U0QWU0TWU-jeUe1_R-TWYi1y2o1_Rkx1IsHy00010rtaNGU0VggjSs23___y1u2015W3xQXGSac_CA8gUd5NCrWGbM6U64bn4vGcvcuPlPJLhtuIGZE_g2rS4r9G1m211CniGnAu4nZWtJVLUopmT0yHPAPsFcn073W00~1' \
	-H 'User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:101.0) Gecko/20100101 Firefox/101.0' \
	-H 'Cookie: yandexuid=239691761638459990; _ym_uid=16424911621068028391; device_id=a16785f23e2bbbed709ffcf22743df315354d6341'
```

CURL с примером для click_url:

```
curl 'https://yabs.yandex.ru/count/WrKejI_zOF82NHe052v6BCNgZPchDmK0yWCGWY0nQxjMOW00000uhFHs0d2KWzEZdgAXyyi1W06Il_m2Y06GxBs0Z06G0VBsdOFPW8200fW1ylQTWrcu0QpMhgKam042s06sz-2a0U01jFJWf07e0TW1e0A0_EWMy0BjwAhq3803tBgGsWc80ysJfNQO0yd44g031AW3A87l0lW4_zfGY0N_sb2G1V6UhWAW1UhF6AW5my8Ki0N3mXIu1TFhJC05rEE_0SW5z-0mrl2b2i46LaeC96EEKmF9gGUarBJ8RVa-6h07W82OFBW7W0NW1uOAyGTS7KIRpKd93e0810ZW282-j0le2Sa8GFWAWBKOgWiGRzrgkQJK002LyL3jXzm50DaBw0l_sb3m2mg83AIcthu1gGnGQtJaWxxYF-WCbq293i7AeKMsyzMW3i24FGX0W13R-TWYa13XWDQDvQtqWoeGD3CpCpCpund0pzNdUKu_iHAo3biupORaF-aIyuQxly9M_QJm4X3W4_kzam6W5Fkzam6e5AYDn0J0582YbH7850VsuR6I1kWKX0BG5VRXiP86s1N1YlRieu-y_6Fme1Q8bDgI1iaMy3_G5gIcthu1WHUO5u6wpYwe5md05xGMq1VGXWFO5w35FPaOe1WCi1ZfrDgI1j0O4FWO-fweszJLkh9uW1c0wONvZypeZeW1a1a1e1cmg06m6TQKiQ2opEEf0xWPqXaIUM5YSrzpPN9sPN8lSZOrCYqrw1c0mWFm6O320u4Q__-dMO4eMSI86i24FPWQ_F280h0QoVkkzyFRW8WCk1e6zHe10000WXiWCJPZDJSpCM4pPM9ZD3aqP3bcOs4rE3LbOs8uPMCsC36m6sIu6mNf6m00040M41X1y1lfqbw270qmOK4wD75LOrLPLLatwHo07Vz_cHsW7W6e7W7O7lhQ7g0Vs_dO8h0V0iWVsxkmKjaV0000GDTv5q7W7wghNDWW____0U0W0I00-seK799FBsE96I4oOsR3Y2A3Xapm6nANBIzPoBZ276SzceUaoI5PeApePnZMcZFOfOGCjbUVNIQW1XWX1l5mn45SRUNp8aWO38nnpflglP1Gns0jnVTHwat4FK0JQ7Ngb0EX42SF~1?etext=&from=&q=%D0%B5%D0%B4%D0%B0' \
	-H 'User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:101.0) Gecko/20100101 Firefox/101.0' \
	-H 'Cookie: yandexuid=239691761638459990; _ym_uid=16424911621068028391; device_id=a16785f23e2bbbed709ffcf22743df315354d6341'
```

<a id="advert-objects"></a>

## Какие объекты сейчас могут быть "рекламными"

Объект рекламный, если у него есть ссылки на счетчики просмотров и кликов.

На данный момент такими объектами могут быть:

- Рестораны в виджетах
  [layout-constructor](https://bb.yandex-team.ru/projects/EDA/repos/spec-api/browse/specs/client_layout-constructor_v1/widgets/widgets.yml#1264)
- Рестораны в
  [ответе](https://bb.yandex-team.ru/projects/EDA/repos/spec-api/browse/specs/client_full-text-search_v1/spec.yml#354)
  ручки поиска
- Баннеры в
  [ответе](https://bb.yandex-team.ru/projects/EDA/repos/spec-api/browse/specs/client_banners_v1/spec.yml#287)
  eats-layout-constructor (спека смотрит по ссылке, не удивляйтесь)

<a id="problems"></a>

## Какие бывают проблемы с событиями/рекламными ссылками

Антифрод может посчитать, что переход по ссылке был некорректный. Такие события
называются "зафроженными".

Типичные проблемы, по которым антифрод может так посчитать:

- событие клика случилось раньше чем событие просмотра
- для события клика не было события просмотра
- событие не было привязано к пользователю (антифрод не смог идентифицировать
  пользователя и решил, что это аноним)
- событие клика или просмотра произошло из внутренней сети яндекса

<a id="client-behaviour"></a>

## Как нужно работать с ссылками клиентам

За сессию для одного рекламного объявления событие одного вида может быть
отправлено только один раз. Т.е.: максимум 1 просмотр и 1 клик для одного
рекламного объявления. Сессия сбрасываетcя при "pull-to-refresh", смена адреса,
смена пикера (тайпикер), смена фильтра.

**Важно**: гарантировать порядок "продергиваний" ссылок. Просмотр всегда должен
быть раньше клика. Если события просмотра для объявления еще не произошло, но
пользователь собирается перейти по объявлению (в т.ч. дернуть клик), то
просмотр нужно дернуть форсированно. По кликовой ссылке нужно перейти, даже
если просмотровая вернула ошибку (или упала по сети).

Дернуть view_url нужно в случае, если сошлись все следующие условия:

- объявление попало во view-port на определенный процент своего контента
  (`view_threshold`)
- и нахождение во view-port больше этого порога дольше порога времени
  (`viewed_time` - секунды)

Параметры задаются конфигом:
[eda_ads_parameters](https://tariff-editor.taxi.yandex-team.ru/experiments3/experiments/show/eda_ads_parameters)

**Важно**: в некоторых объявлениях, например в баннерах, одна из ссылок может
не прийти с бека, т.к. по спеке они опциональны. Нужно это учитывать, с
оглядкой на спеку, естественно, и в случае если:

- не пришла просмотровая ссылка, то дергать только кликовую
- не пришла кликовая ссылка, дергать только просмотровую

Про политику ретраев: ретраи делать не нужно.

<a id="client-behaviour-examples"></a>

### Примеры

1. viewed_time = 1; view_threshold = 0.4
   Ресторан находился полностью на экране больше 1 секунды - отправили
   просмотр
2. viewed_time = 1; view_threshold = 0.4
   25% ресторана видно на экране больше 1 секунды - ничего не отправили, т.к.
   не сработал порог по доле объявления во view-port
3. viewed_time = 1; view_threshold = 0.4
   25% баннера видно на экране больше секунды - ничего не происходит
   прокрутили вниз до момента, как баннер видно на половину и подождали еще
   секунду - отправили просмотр
4. viewed_time = 1; view_threshold = 0.4
   25% баннера/ресторана видно на экране меньше секунды и нажали на объявление
   - отправили просмотр, а потом клик

<a id="client-behaviour-send-delay"></a>

### Про задержку в отправке событий

По-хорошему, чем меньше времени прошло между событием (фактический показ/клик)
и отправкой события (продергивание показ/клик ссылок) - тем лучше.

Минимизируя время между продергиванием урла и фактическим временем события, мы
даем честную информацию о произошеддшем баннерной крутилке. Грубо-говоря, если
мы в конце сессии отправим все просмотры скопом, то обманем БК, т.к. она будет
считать, что вот только сейчас эти просмотры случились и при том одновременно,
хотя фактически между просмотром_1 и просмотром_2 могло пройти существенное
время.

<a id="client-behaviour-send-params"></a>

### Какие параметры нужно передавать при продергивании ссылок (речь про заголовки)

Критично важно передавать все куки - по ним баннерная крутилка определяет
пользователя. Это чинит фильтр антифрода, который срезает анонимных
пользователей.
Также важно передавать `User-Agent` и `Referer`.

Список заголовков, которые нужно отправлять:

- Cookie
- User-Agent
- Referer (если есть)
- x-appmetrica-uuid (если есть)
- x-mobile-ifa (если есть)


<a id="links-and-sources"></a>

## Ссылки и источники

- https://wiki.yandex-team.ru/users/janual/eda-ads/#rabotasdirektom (немного
  deprecated)

