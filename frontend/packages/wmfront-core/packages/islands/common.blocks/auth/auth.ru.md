## Описание
Блок **auth** – форма авторизации на сервисах Яндекса. Позволяет авторизоваться как с логином и паролем, так и с аккаунтом внешней социальной сети.

Предоставляет возможность:
     
 * зарегистрироваться на Яндексе;
 * авторизоваться в [Яндекс.Паспорте](http://doc.yandex-team.ru/Passport/AuthDevGuide/concepts/about.xml) с помощью аккаунта Яндекса (логин/пароль) или аккаунта одной из поддерживаемых Паспортом социальных сетей (Twitter, Facebook, ВКонтакте, Одноклассники, Mail.ru или Google);
 * автоматически разлогиниться после закрытия браузера (при выбранной опции **Чужой компьютер**); 
 * напомнить пароль;
 * проверить корректность введенных пользователем данных;
 * показать сообщения об ошибках;
 * задать расположение элементов формы в соответствии с требованиями сервиса.
   
Форма располагается внутри блока [«Домик авторизации»](../domik/domik.ru.md).  

Для дополнительной безопасности передачи данных при авторизации использует HTTPS. Безопасность можно [отключить](#unsecurity).

## Техническое описание
### Структура блока
<a name="allelems"></a>
#### Элементы блока 

Большинство элементов блока формируются за счет других блоков: `input`, `button`, `link`, `checkbox`.

**Необязательные элементы:**

---
**NB** С версии islands 4.x все элементы блока опциональные. При использовании самостоятельно подключите в зависимости блока.

--- 

* `username` — поле ввода логина.   
Допустимые значения: `-а-яА-ЯёЁA-Za-z0-9` – латинские и кириллические буквы верхнего и нижнего регистров, а также  цифры.
Например, в качестве логина при необходимости может быть указан адрес электронной почты, заданный в сервисе [ПДД](https://pdd.yandex.ru/domains_add/).
* `password` — поле ввода пароля.  
 Допустимые значения: ```-a-zA-Z0-9`!@#$%^&*()_=+[]{};:"|,.<>/?```
* `button` — кнопка «Войти».
* `error` — сообщение об ошибке, создается при необходимости;
* `haunter` — опция «Чужой компьютер», по умолчанию не выбрана;
* `register` — ссылка «Регистрация», ссылка на страницу регистрации;
* `remember` — ссылка «Напомнить пароль», ссылка на страницу восстановления пароля;
* `social` — элемент для социальной авторизации, содержащий иконки социальных сетей;
* `social-icon` — иконки социальных сетей;
* `social-popup` — выпадающее окно c социальными иконками;
* `hidden` — элемент для добавления в форму скрытых параметров. Имя и значение параметра передаются через BEMJSON-поля `name` и `val`.

* `row` — псевдоэлемент, позволяющий сверстать несколько элементов в ряд.  

_При использовании опциональных элементов (в отсутствие модификатора `content` со значением `auto`) необходимо самостоятельно подключить нужные элементы в зависимости блока. 
Если используете вместе с модификатором `content` со значением `auto`, то дополнительно подключать опциональные элементы нет необходимости._


```js
{
    block: 'auth',
    mods: {content: 'auto'},
    content: [
        {elem: 'username'},
        {elem: 'password'},
        {elem: 'button'},
        {elem: 'hidden', name: 'enough', val: 'оливье'},
        {elem: 'hidden', name: 'letsgo', val: 'танцевать'}
    ]
}
```
 
#### Социальная авторизация 
--- 
 **NB** Для авторизации через социальную сеть на компьютере пользователя должен быть включен JavaScript.

---

DOM-узлы элемента `social` создаются на клиенте во время инициализации блока.
Содержимое элемента строится на клиенте, но описывать его нужно заранее:

```javascript
{
    block: 'auth',
    …
    content: [
        …
        { elem: 'social' }
        …
    ]
}
```   

Блок не содержит данных о том какие социальные сети использовать.
Необходимая информация возвращается в ответ на AJAX-запросы в Паспорт, отправляемые при каждом создании формы на клиенте. В Паспорте определяется список используемых иконок социальных сетей, последовательность, а также какие из них должны быть спрятаны в выпадающее окно (появляется при нажатии кнопки с многоточием).

Поддержка каждого социального сервиса требует изменений со стороны Паспорта и появляется у всех сервисов Яндекса одновременно.

Авторизация происходит после клика на иконку. Открывается выпадающее окно с загруженной социальной сетью. В случае успешной авторизации исходная страница обновляется.

Связь с социальными сервисами обеспечивает [Социальный брокер](https://wiki.yandex-team.ru/social/broker), разработанный в Паспорте. Взаимодействие с Брокером выполняется через блок [social-broker](../social-broker/social-brocker.ru.md).

Для социальной авторизации блок использует значения глобальных параметров из [i-global](../i-global/i-global.ru.md):
  
* `social-host` — адрес в Паспорте, откуда берется информация об иконках. Если не задан, то социальная авторизация отключается.
* `social-sprites` — поле `icon_sprites` в данных, полученных из Паспорта.
* `social-providers` — поле `providers` в данных, полученных из Паспорта.

#### Модификаторы блока
##### Автоматическое содержимое

Модификатор `content` со значением `auto` автоматически формирует содержимое блока. В результате создается простая форма авторизации, которая подойдёт в большинстве случаев. 

Если у блока не задано поле `content`, то его содержимым станут все [элементы формы](#allelems):  необязательные и социальная авторизация.

**NB** По умолчанию в модификаторе подключены в зависимости все [элементы](#allelems) блока.

```js
{
    block: 'auth',
    mods: {
        content: 'auto'
    }
}
```
 
При установленном модификаторе существует возможность задать только нужные элементы формы в поле `content` блока. Если у данных элементов будет пустое содержимое, то оно построится автоматически с данными по умолчанию.

```js
{
    block: 'auth',
    mods: {content: 'auto'},
    content: [
        { elem: 'username' },
        { elem: 'password' },
        { elem: 'button' }
    ]
}
```

Текст на элементах локализуются автоматически (необходима сборка локализованных файлов).

---
**NB** Рекомендуется использовать автоматическое содержимое установив модификатор `content` со значением `auto`. 

---

Если модификатор не указан, необходимо описать содержимое нужных элементов формы в поле `content`.

### API блока
<a name="bemjson"></a>
#### BEMJSON-поля

* `{String} url` — адрес сценария на веб-сервере, который обрабатывает данные формы (`<form action="url"/>`). В качестве метода для отправки данных (атрибут формы `method`) всегда используется `POST`. Необязательное поле. Значение по умолчанию: `https://passport.yandex.ru/passport?mode=auth&twoweeks=yes`. 

  Адрес по умолчанию формируется из параметров блока `i-global`:

  * `passport-host` — хост Паспорта;
  * `passport-msg` — ID сервиса, c которого пользователь осуществляет вход. 

* `{Array} content` – содержимое блока. Обязательное, если не установлен модификатор `content` со значением `auto`. 

* [элементы блока](#allelems). Содержимое каждого элемента формируется в соответствующем поле `content`. 
*  `{String} name`, `{String} val` - имя и значение, для добавления в форму скрытых параметров (элемент `hidden`).

* `{String} retpath`, `{String} from`, `{String} origin`, ` {String} timestamp` — поля для передачи значений соответствующим скрытым полям формы (`<input type=hidden>`).

Поле `origin` используется для обозначения места авторизации/регистрации на сервисе и сам сервис. Если на сервисе можно авторизоваться в нескольких местах, то чтобы их различать — каждому нужно задать отдельный `origin`. Кроме того, если место входа или форма регистрации отличается для `desktop` и `touch`, то их также нужно разделить с помощью `origin`. 

Например (формат): `origin=market, origin=market.domik, origin=market.cart`.

  По умолчанию значения полей `retpath` и `from` определяются из блока `i-global`. Если значения полям явно не переданы и значений по умолчанию нет, то будут добавлены поля с пустыми значениями.

  Значение полю `timestamp`, как правило, передавать не нужно, так как оно используется в [JS](#unsecurity) в момент отправки формы.
 
```js
{
    block: 'auth',
    mods: {content: 'auto'},
    origin: 'serp.domik',
    retpath: 'https://yandex.ru/search/?text=котятки'
}
```

<a name="unsecurity"></a>
#### JS
#### Безопасность
Для безопасной передачи данных в блоке используется HTTPS.

По умолчанию перед отправкой данных создается DOM-узел содержащий время отправки формы:

```html
<input type="hidden" name="timestamp" value="…"/>
```
Значением поля является количество секунд, прошедших с начала эпохи (`+new Date()`).

Данный способ повышает безопасность. Однако, его можно отключить если на сервере нет проверки времени или если подобное поведение нежелательно.

Безопасность отключается переопределением метода `_onSubmit()`.
