# Viper configuration

Configuration via https://github.com/spf13/viper

## Example

```
import (
	"testing"

	"github.com/YandexClassifieds/go-common/conf"
	"github.com/YandexClassifieds/go-common/conf/viper"
)
	
func main(){
  c := viper.NewConf()
  funcExample(c)
}

func funcExample(c conf.conf){
  ...
  envValueDI := c.Str("ENV_KEY")
  // or
  envValueGlobal := conf.Str("ENV_KEY")
  ...
}
```

```
func Test(t *testing.T) {
  conf := conf.NewTestConf()
  ...
}
```

## Description

- Конфигурация для работы приложения основывается на переменных окружения.
- Поддерживает загрузка файлов конфигурации для локальной разработки и тестов.
- Для сборок в CI требуется передать переменную окружения `CI=true`  
- Секреты нужно приносить локально в ручную (точка роста)
- Отсутствие переменной окружения вызовет панику. Это позволяет гарантировать ожидаемое поведение и единое место конфигурации. 
Однако для особых случаев можно сделать явный `conf.Exist()`

## Development and tests

Для локальной разработки и тестов необходимо положить три файла:
- `dev.env` - окружение для локальной работы приложения
- `test.env` - окружение для запуска тестов локально и в CI
- `local.env` - секреты

Файлы могут быть как общие, для этого они должны находиться в корне проекта, 
так и локальные, для этого они должны находиться в `/cmd/service_name` или в `/pkg`