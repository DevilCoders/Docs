# Backtrace

Содержит несколько функций:
* `currentBackTrace` — бектрейс текущего исключения в виде строки
* `currentExceptionMessage` — сообщение текущего исключения + бектрейс
* `exceptionMessage` — сообщение переданного исключения + текущий бектрейс (для использования внутри `catch`)

Всё это может стать ненужным, когда трейс появится в `CurrentExceptionMessage`.

Однако помимо функций тут пирдирятся:
* [`library/cpp/dwarf_backtrace/registry`](/arc/trunk/arcadia/library/cpp/dwarf_backtrace/registry) — для вывода имён файлов
* [`library/cpp/terminate_handler`](/arc/trunk/arcadia/library/cpp/terminate_handler) — для регистрации обработки непойманных исключений

## Использование

Необработанные исключения автоматически включат бектрейс. Для явной распечатки куда-нибудь (например, в [`log8`](/arc/trunk/arcadia/maps/libs/log8)), нужно их ловить:

```cpp
#include <maps/analyzer/libs/backtrace/include/backtrace.h>

int main() {
    try {
        myFunction();
    } catch (const std::exception& e) {
        // По сути то же, что и `currentExceptionMessage`, который можно использовать в `catch ( ... )`
        ERROR() << maps::analyzer::exceptionMessage(e);
    }
}
```
