# Yandex.Drive backend style guide

## C++
Основной styleguide, принятый в Аркадии: https://docs.yandex-team.ru/arcadia-cpp/cpp_style_guide
- Оператор ```new``` не должен использоваться – вместо него сразу создается умный указатель с помощью ```MakeHolder<T>(...)```, ```MakeAtomicShared<T>(...)```. В существующем коде это правило можент нарушаться, т.к. legacy
- Стоит использовать ```namespace NDrive { ... }``` для организации кода. Допустимо использовать еще один уровень пространств имен, например ```namespace NDrive::NChat { ... }```
- Там, где это возможно, нужно использовать **forward declaration** protobuf'ов
- Использование макросов должно быть минимальным. Исключение – макросы ```R_FIELD, R_OPTIONAL``` для создания полей с accessor'ами
- Тяжелые шаблонные классы стоит разделять на определение в **\<name\>.h** файле и реализацию в **\<name\>_impl.h** файле
- POD-like типы стоит передавать по значению, например, ```TInstant, TStringBuf```
- При передаче аргументов по значению не стоит писать ```const int param``` – компилятор выкидывает const

## Обработка ошибок
### Legacy
По историческим причинам обработка ошибок в большей части кода осуществляется с помощью кодов возврата (а именно возврата ```bool``` или ```optional<Result>```), при этом ошибка пишется в специальный объект ```NDrive::TEntitySession```, который содержит в себе и ошибки, и транзакцию в базу данных. То есть сигнатура функции обычно выглядит как
```
[[nodiscard]] bool DoSomething(const TArgs& args, NDrive::TEntitySession& tx);
```
или
```
TMaybe<int> CalcSomething(const TArgs& args, NDrive::TEntitySession& tx);
```
Правила написания кода в таком стиле:
- Если функция вовращает ошибку (```return false``` или ```return {}``` для ```TMaybe```) и в нее передается ```NDrive::TEntitySession```, то можно считать, что эта функция уже выставила ошибку (позвала ```tx.SetErrorInfo(...)```). Вызывающий такую функцию код может лишь уточнить ошибку с помощью ```tx.AddErrorMessage(...)```
- Лучше принимать ```NDrive::TEntitySession&``` снаружи, чем создавать внутри свой
- Чтобы избежать игнорирования кода возврата нужно использовать ```[[nodiscard]]```
- Если функция, принимающая ```NDrive::TEntitySession```, вернула ошибку, то нужно стремительно делать ```return false/{};``` по стеку вызовов

Пример:
```
[[nodiscard]] bool Foo(int arg, NDrive::TEntitySession& tx) {
    if (arg > 42) {
        tx.SetErrorInfo("Foo", "argument value is too big");
        return false;
    }
    return true;
}

TMaybe<int> Bar(int arg, NDrive::TEntitySession& tx) {
    if (!Foo(arg, tx)) {
        // tx.SetErrorInfo("Bar", "bad Foo return"); – неверно, Foo уже выставил ошибку
        tx.AddErrorMessage("Bar", "bad Foo return"); // Ok
        return {};
    }
    return arg + 42;
}
```

### Exceptions
Для кидания исключений предусмотрен макрос ```R_ENSURE```:
```
#define R_ENSURE(
    CONDITION /* условие, можно использовать любое выражение, кастующееся к bool*/,
    CODE /* HTTP-код ошибки, можно использовать {}, если код ошибки был уже установлен в EntitySession */,
    DEBUG_MESSAGE /* сообщение об ошибке, можно использовать оператор << */,
    TX /* опциональный объект NDrive::TEntitySession, нужно указывать, если таковой имеется в текущем scope */
)
```

Примеры использования
```
R_ENSURE(finishedTask || !api->HasBillingManager(), HTTP_INTERNAL_SERVER_ERROR, "cannot AddClosedBillingInfo: " << finishedTask.GetError());

R_ENSURE(optionalSession, {}, "cannot GetSession " << finishedSessionId, tx);

R_ENSURE(session, HTTP_INTERNAL_SERVER_ERROR, "null session in NotifyPassport", tx);
```

## Соглашение об именовании ручек
Ручки именуются следующим образом:
```
/api/<тип авторизации>/<сущность>/<подсущность>/<глагол>
```
например:
```
/api/leasing/user/edit
/api/leasing/user/document-photo/list
/api/staff/car/tag/remove
```
- Не все ручки соответствуют этому формату т.к. legacy
- Cтоит использовать `-` в именах ручек, не `_`
