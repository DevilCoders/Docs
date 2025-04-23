Генерация TypeScript definitions и controller stub для Spring MVC контроллеров
==============================================================================
Релизится через [ЦУМ](https://tsum.yandex-team.ru/pipe/projects/jlibrary/delivery-dashboard/market-libraries).

Версии можно посмотреть вот тут: 
* [springmvc-to-ts-codegeneration](http://artifactory.yandex.net/yandex_market_releases/ru/yandex/market/springmvc-to-ts-codegeneration/)
* [springmvc-to-ts-annotations](http://artifactory.yandex.net/yandex_market_releases/ru/yandex/market/springmvc-to-ts-annotations/)

Репозиторий для `gradle` плагина: https://github.yandex-team.ru/market-java/springmvc-to-ts

Цель проекта
----
Основная задача модуля - получить список пакетов с контроллерами (`@Controller`/`@RestController`) и сгенерировать
файл `java-definitions.ts`, в котором будут `interface`-ы для всех используемых POJO, и `stub`-ы для контроллеров.

Т.е. для
```java
@RestController
class SampleController {
    @GetMapping("/api/usefull-method/{id}/")
    public SampleResult processSample(@PathVariable("id") int id, @RequestParam("intData") String intData) {
        // ...
    }
    
    public static class SampleResult {
        @Nullable
        private String name;
        private int cnt;
        // ...
    }
}
``` 

Получится
```typescript
class SampleController {

  constructor(private fetchApi: FetchAPI) {
  }
  
  processSample(id: number, intData: string): Promise<SampleResult> {
    return this.fetchApi(`/api/usefull-method/${id}`, {
      method: RequestMethod.POST,
      qs: {intData},
      responseType: ResponseType.JSON,
    });
  }
}

interface SampleResult {
  name?: string;
  cnt: number;
}
```

Который дальше можно использовать в своём коде для взаимодействия с бэкендом.

Подключение к проекту
---------------------

Добавить в `ya.make`:
```shell script
# генеруем недостающий файл generated/definitions.ts
RUN_JAVA_PROGRAM(
    ru.yandex.market.springmvctots.codegen.MvcToTsMain --config-file ts_codegen_config.json --output-file ${BINDIR}/generated/src/rest/definitions.ts
    IN ts_codegen_config.json
    OUT_DIR ${BINDIR}/generated
    CLASSPATH market/jlibrary/springmvc-to-ts/springmvc-to-ts-codegeneration market/mbo/content-lab/content-lab-ui/src/main
)

# добавляем его в сорцы проекта
JAVA_SRCS(SRCDIR ${BINDIR}/generated src/rest/definitions.ts)
```

Использования на фронте
-----------------------

Из каробки также поставляется функция `createFetchApi`. С ее помощью не нужно думать как отправить запрос и обработать ответ.

Пример простого использования:

```typescript
import { createFetchApi, SampleController } from './java/definitions';

const fetchApi = createFetchApi();
const samleService = new SampleController(fetchApi)

samleService.someMethod().then(data => {
  //...
})
```

Также можно заменить стандартный `fetch` своей функцией:

```typescript
import { createFetchApi } from './java/definitions';
import fetchPolyfill from 'fetch-polyfill';

const fetchApi = createFetchApi({
  customFetch: (url: string, options?: RequestInit) => {
    
    return fetchPolyfill(url, options);
  }
});
```

Также есть `middleware`, которые позволяют трансформировать запрос или ответ:

```typescript
import { createFetchApi } from './java/definitions';

const fetchApi = createFetchApi();

fetchApi
    .before(({ url, options, requestOptions }, next) => next({
      url,
      requestOptions,
      options: {
        ...options,
        credentials: 'include',
      },
    }))
    .after(({ request, response, result }, next) => {
      console.log(request, response);

      // Лучше клонировать, чтобы в других middleware можно было вызвать response.json() и т.д.
      const cloneResponse = response.clone();
      
      return next({
        request,
        response,
        // Примичание: если после выполнения всей цепочки middleware,
        // result будет равен undefined,
        // то стандартная трансформация ответа не будет выполнена
        // и result вернется в качестве результата выполнения запроса
        result: cloneResponse.blob(),
      });
    })
```

# Локализация enum

Бывает, что вместе с enum нужно также экспортировать в typescript какие-то связанные данные. Например, локализация 
значений. Для этого объявите метод и пометьте его аннотацией:
```java
    public static enum Role {
        ADMIN("Администратор", "Administrator"), GUEST("Гость", "Guest");
        private final String ru;
        private final String en;

        Role(String ru, String en) {
            this.ru = ru;
            this.en = en;
        }

        @TsExportEnumConverter
        public String getRu() {
            return ru;
        }

        @TsExportEnumConverter
        public String getEn() {
            return en;
        }
    }
``` 

В TypeScript будет выглядеть так:
```typescript 
export class RoleConverters {

  static getEn(value: Role): string {
    switch (value) {
      case Role.ADMIN:
        return 'Administrator';
      case Role.GUEST:
        return 'Guest';
    }
  }

  static getRu(value: Role): string {
    switch (value) {
      case Role.ADMIN:
        return 'Администратор';
      case Role.GUEST:
        return 'Гость';
    }
  }
}
```  

Если функция не будет чистой, то будут прикопаны результаты на момент компиляции. Не делайте так.

Бывает так, что модифицировать enum нет возможности, например, если это сгенерированный код. В этом случае реализуйте 
интерфейс:

```java 
public class GetEn implements EnumConverter<Role, String> {
   @Override
   public String convert(Role role) {
      return role.getEn();
   }
}
```

Результат будет похожий.

Нюансы
======
На сегодняшний день генерирует один большой `definitions.ts` со всеми классами/интерфейсами. Это по большей части ограничение используемой библиотеки. Потенциально можно попробовать сделать распихивание по пакетам, но это потребует прописывания импортов внутри генерируемого кода и немного более сложной работы с записью результатов.

Для небольших проектов один большой `definitions.ts` вполне нормальный вариант (по своему даже удобный). Для больших (для большого MBO, скажем) потребуется решить этот вопрос.

Если нужна поддержка IE11, то необходимо использовать полифилы для `fetch` и `URLSearchParams`
