# Сваггер

## Инициализация

Инициализация сваггера в [main.ts](../lib/main.ts) в функции Bootstrap:

```typescript
const swaggerConfig = new DocumentBuilder()
    .setTitle(config.swaggerTitle)
    .setVersion(config.appVersion)
    .addTag('posts')
    .addTag('main')
    .addTag('tags')
    .addTag('categories')
    .addTag('polls')
    .addTag('internal')
    .build();
const document = SwaggerModule.createDocument(app, swaggerConfig);

SwaggerModule.setup('swagger', app, document);
```

* `setTitle` - заголовок страницы сваггера
* `setVersion` - версия страницы сваггера
* `addTag` - добавляет тэги, для контроллеров

---

## Контроллеры

`SwaggerModule` автоматически отображает эндпоинты проекта по умолчанию.

Для того, чтобы указать, к какой категории относятся ручки контроллера используется декоратор `@ApiTags()`

```typescript
@ApiTags('tags')
@Controller('tags')
export class TagController {
    constructor(private readonly tagService: TagService, private readonly getTagTransformer: GetTagTransformer) {
    }
}
```

---

## Ручки

### Декораторы для ручек

`SwaggerModule` ищет все декораторы `@Body()`, `@Query()`, и `@Param()` в ручках и генерирует API-Документы на их основе.

* `@ApiQuery()` - конфиг для описания query запроса
* `@ApiBody()` - конфиг для описания body запроса
* `@ApiResponse()` - конфиг для описания типа ответа

```typescript
export class TagController {
@Get(':urlPart')
    @ApiQuery({type: PublicTagQuery})
    @ApiResponse({status: 200, description: 'get tags', type: PublicTagResponse})
    get(@Req() req: Request, @Param('urlPart') urlPart: string, @Query() query: IGetPublicTagQuery): Promise<IGetTagTransformedTag | IPublicTag | null> {
        return this.getTagTransformer.transform(tag);
    }
}
```

---

## Типы
В качестве типов [nest-swagger](https://docs.nestjs.com/openapi/introduction) принимает классы.

Договорились класть сваггеровские типы в `journal-api/lib/types/swagger-types`
Все файлы для типов сваггера должны содержать в названии `*.entity.ts`, чтобы сваггер-модуль преобразовал большее кол-во простых типов в этих файлах.

---


### Примитивы
Основной декоратор для описания поля класса `ApiProperty()`

```typescript
// Тип содержит в себе поле - строку
import {ApiProperty} from "@nestjs/swagger";

class EntityWithString {
    @ApiProperty()
        name: string;
}
```

Примитивы будут преобразовываться корректно:

```typescript

// Лежит в файле tag.entity.ts поэтому SwaggerPlugin автоматически распарсит несложные типы
// Типы будут корректными без использования ApiProperty()
class Tag {
    urlPart: string;
    title: string | null; // все еще будет работать
    isHot: boolean;
}

```

Хинт:
`pages: string | number | null;` с двумя разными примитивами помимо null работать уже не будет.

---
Более подробное описание свойства через декоратор:

```typescript
// Тип содержит в себе поле - кол-во
import {ApiProperty} from "@nestjs/swagger";

class EntityWithNumber {
    @ApiProperty({
        type: Number,
        description: 'Количество',
        minimum: 1,
        default: 1,
        required: true,
        nullable: false,
    })
    quantity?: number;
}
```

Вместо указания ключа `@ApiProperty({ required: false })` можно использовать декоратор `@ApiPropertyOptional()`.

---

### Типы посложнее

Как описать типы посложнее.

* Массивы:

```typescript

// Все три способа работают
class Entity {
    @ApiProperty({type: [String]})
    names: string[];

    // предпочтительный, т.к. позволяет без проблем описывать массивы классовых типов.
    @ApiProperty({type: String, isArray: true})
    names: string[];

    // позволяет описать массив, внутри которого могут быть разные типы, см. далее
    @ApiProperty({
        type: 'array',
        items: {
            type: String
        }
    })
    names: string[];
}
```

* Двумерные массивы:
```typescript

class Entity {
    @ApiProperty({
        type: 'array',
        items: {
            type: 'array',
            items: {
                type: String
            }
        }
    })
    namesOfNames: string[][];
}
```

* Вложенные типы:

Категории содержат в себе массив тэгов

```typescript
class Tag {
    urlPart: string;
    title: string | null;
    mmm: string | null;
    isHot: boolean;
}

export class Category {
    urlPart: string;
    title: string | null;
    @ApiPropertyOptional({ type: Tag, isArray: true }) // В идеале всегда описывать вложенный тип при помощи ApiProperty()
    tags?: Tag[];
}
```

* Enum-ы

Можно по простому описать интересующие значения
```typescript
class SomeEntity {
    @ApiProperty({ enum: ['Admin', 'Moderator', 'User']})
    role: UserRole;
}
```

или указать енум как тип, через свойство `enum`

```typescript
enum UserRole {
    Admin = 'Admin',
    Moderator = 'Moderator',
    User = 'User',
}

class User {
    name: string;
    @ApiProperty({name: 'role', enum: UserRole, default: 'User'})
    role: UserRole = UserRole.User
}
```

* OneOf типы через не описать через `|`

Нужно импортировать эти типы и добавить классу, который будет их использовать, декоратор и добавить импортированные типы как его переменные
Затем, указать их по рефу через `getSchemaPath`

```typescript
import {ApiProperty, ApiExtraModels, getSchemaPath} from "@nestjs/swagger";

export class TextBlock implements ITextBlock {
    @ApiProperty({ type: String })
    type: 'text';
    text: string;
}

export class CodeBlock implements ICodeBlock {
    @ApiProperty({ type: String })
    type: 'code';
    code: string;
}

export class AutoImageBlock implements IAutoImageBlock {
    @ApiProperty({ type: String })
    type: 'imageWithDescription';
    @ApiProperty()
    imageWithDescription: {
        type?: ImageType;
        image?: AvatarsImage;
        imageTitle?: string;
        description?: string;
    };
}

@ApiExtraModels(TextBlock, CodeBlock, AutoImageBlock)
export class AutoCardWithImagesTransformedBlock implements IAutoCardWithImagesTransformedBlock {
    @ApiProperty()
    type: 'cardWithImages';
    @ApiProperty({
        oneOf: [{ $ref: getSchemaPath(TextBlock) }, { $ref: getSchemaPath(CodeBlock) }, { $ref: getSchemaPath(AutoImageBlock) }],
    })
    cardWithImages: TextBlock | CodeBlock | AutoImageBlock;
}
```

Если нужно описать полиморфный массив `Array<Cat | Dog | Bird>;` задать в @ApiProperty() тип `array`, а уже у него в items указать oneOf типы

```typescript
@ApiExtraModels(TextBlock, CodeBlock, AutoImageBlock)
export class AutoCardWithImagesTransformedBlock implements IAutoCardWithImagesTransformedBlock {
    @ApiProperty()
    type: 'cardWithImages';
    @ApiProperty({
        type: 'array',
        items: {
            oneOf: [{ $ref: getSchemaPath(TextBlock) }, { $ref: getSchemaPath(CodeBlock) }, { $ref: getSchemaPath(AutoImageBlock) }],
        },
    })
    cardWithImages: Array<TextBlock | CodeBlock | AutoImageBlock>;
}
```
