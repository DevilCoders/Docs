# PBSN Reader

Читатель pbsn для golang.

## Использование

``` go
import (
    "a.yandex-team.ru/market/idx/golibrary/pbsn"
    "log"
    "os"
)

<...>
// Файл, содержащий сообщение SomeProtoMessage с магической подписью "SOME"
file, err := os.Open("file.pbsn")
if err != nil {
	log.Fatal(err)
}

// pbsn.NewReader принимает любой объект, удовлетворяющий интерфейсу io.Reader
// Например, таким объектом может быть файл. Или обёртка над байтовым массивом
reader := pbsn.NewReader(file)
message := &SomeProtoMessage{}
err := reader.CheckMagicAndParseProto("SOME", message)
if err != nil {
	log.Fatal(err)
}
// Работа с message
```

## Обработка нескольких сообщений

``` go
import (
    "a.yandex-team.ru/market/idx/golibrary/pbsn"
    "io"
    "log"
)

func ProcessFile(file io.Reader) error {
    reader := pbsn.NewReader(file)
    for {
        message := &SomeProtoMessage{}
        if err := reader.CheckMagicAndParseProto("SOME", message); err == nil {
            // Process message
        } else if err == io.EOF {
            return nil
        } else {
            return err
        }
    }
}
```

## Переиспользование ридера

``` go
import (
    "a.yandex-team.ru/market/idx/golibrary/pbsn"
    "io"
    "log"
)

func ProcessFiles(files []io.Reader) error {
    reader := pbsn.NewReader()
    for _, file := range files {
        for {
            message := &SomeProtoMessage{}
            if err := reader.CheckMagicAndParseProto("SOME", message); err == nil {
                // Process message
            } else if err == io.EOF {
                break
            } else {
                return err
            }
        }
    }
    return nil
}
```

## Использование ридера для получения массива сообщений

``` go
import (
    "a.yandex-team.ru/market/idx/golibrary/pbsn"
    "io"
    "log"
)

func ProcessFile(file io.Reader) error {
    reader := pbsn.NewReader(file)
    messages := reader.ParseMessages("SOME", func() proto.Message { return &SomeProtoMessage{} }

    if err != nil {
        return err
    }

    for _, message := range messages {
        // For process message as SomeProtoMessage use `message.(*SomeProtoMessage)`
    }
}
```

Функцию для создания объектов также можно объявить отдельно и передать в `ParseMessages` по имени.

## Определение типа ошибки

Ошибки, случающиеся при попытке распарсить сообщение можно условно разделить на три части:
1) Ожидаемые (`io.EOF` в конце парсинга)
2) Ошибки ридера
3) Ошибки парсинга (некорректный формат)

Ошибки парсинга могут возникать из разных источников (расхождение магических строк, невозможность разжать сообщение, ошибка десериализации протобуфа и т.д.). Для упрощения понимания, возникла ли полученная ошибка ввиду некорректных данных или же дело в более низкоуровневой ошибке ридера сделана вспомогательная функция `IsPBSNFormatError(err error) bool`. 