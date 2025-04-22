# Yate Externals
Экстернал функции, которые используются в проекте.
Также используется библиотека https://github.com/yandex-ui/yate-stdlib/.

##boolean arr-isfind(scalar/\*data\*/, array/\*array\*/)
Проверяет наличие scalar в array. По сути Array.indexOf().

**Пример:**
```
sfolder = [
     'spam'
     'sent'
     'trash'
     'draft'
     'template'
     'outbox'
]

arr-isfind(.symbol, sfolder)
```

##boolean is-folder(scalar/\*fid\*/, scalar/\*symbol\*/)
Вызывает mFolders.isFolder(fid, symbol). Проверяет соответствие fid symbol.

**Пример:**
```
is-folder('12345', 'spam')
```

##boolean is-my-email(scalar/\*email\*/)
Вызывает ns.Model.get('account-information').isMyEmail(email). Проверяет, принадлежит ли емейл текущему пользователю.

**Пример:**
```
is-my-email('foo@yandex.ru')
```


##boolean regexp-test(scalar/\*string\*/, scalar/\*regexp\*/, scalar/\*flags\*/)
Создает RegExp и вызывает RegExp.prototype.test c переданной строкой в качестве аргумента.

**Пример:**
```
regexp-test('foo', '[a-z]', 'g')
```

##nodeset extend(nodeset, nodeset)

##nodeset folders-sort(nodeset)

##nodeset folders-sort-list(nodeset)

##nodeset get-folder-by-fid-or-symbol(scalar)

##nodeset get-folders-by-fids-or-symbols(nodeset)

##nodeset get-label-by-lid(scalar)

##nodeset get-label-by-name(scalar)

##nodeset get-labels-by-lid(nodeset)

##scalar add-params-to-location(object, scalar, boolean, array)

##scalar color-picker(scalar)

##scalar config(scalar)
Выводит значения из Daria.Config

**Пример:**
```
config('product') == 'INT'
```

##scalar daria-url-attachment(nodeset, scalar, object)

##scalar daria-url-attachment-archive(nodeset, scalar)

##scalar daria-url-docviewer(nodeset, scalar)

##scalar date-format(scalar, scalar, boolean)

##scalar date-get-interval(scalar)

##scalar date-pager-url(object)

##scalar entity(scalar)

##scalar entityify(scalar)

##scalar get-current-page-param(scalar)

##scalar get-disk-resource-name(scalar)

##scalar get-human-size(scalar)

##scalar get-shortcut-label-for(scalar, scalar, boolean)

##scalar has-sid(scalar)

##scalar join(nodeset, scalar, scalar)

##scalar json(nodeset)

##scalar lang2index(scalar)

##scalar phone-number-format(scalar)

##scalar set-time(scalar, scalar, scalar, scalar)

##scalar setting(scalar)
Возвращает значение настройки из Daria.mSettings

**Пример**
```
setting('layout') == '2pane'
```

##scalar translate(scalar, scalar, scalar)

##scalar uid-ends(nodeset)

##scalar url-content-folder (nodeset, boolean)

##scalar url-content-label (nodeset, boolean)

##scalar url-content-message (nodeset)

##scalar url-content-sort (scalar, scalar)

##xml c(scalar, scalar, scalar, scalar, scalar)

##xml event-pretty-date(scalar)

##xml messages-item-format-date(nodeset)

##xml avatar(object)
Регистрация аватарки на загрузку в очереди. Вывод заглушки, либо сразу аватарки, если есть данные.
Вызывает Daria.Recipients.add(params)

```
@param {Object} params
@param {String} [params.mid] MID письма, в котором можно получить ключ для загрузки аватарки по email
@param {String} [params.email] адрес для загрузки аватарки
@param {String} [params.name] имя объекта для вывода монограммы
@param {String} [params.size] размер аватарки
@return {String}
```

**Пример:**
```
avatar({
     'email': email
     'mid': mMessage.mid
     'name': name
     'size': size
     'href': false()
})
```
