# ArticleBlock

Описание структуры колдунщика кода. Колдунщик строится по аналогии с html, но имеет урезанную функциональность и заранее прописанные стили. Таким образом схема разметки колдунщика кода технически является урезанным html, но философски больше похож на Markdown.

Стилизация блока происходит по принципу композиции различных типов блоков.

## Блоки

Каждый блок имеет
    - `type` - описывает поведение блока
    - `children` - список других блоков, либо строк, вложенных в данный блок
    - `color` - цвет текста в блоке (ограниченное множество)
    - `isBold` - признак жирного текста

Поддерживаемы блоки
    - `paragraph` - то же, что и `<p>` в html
    - `code` - блок форматирующий текст как код, может быть инлайн или абзац (по умолчанию)
    - `hr`
    - `list` - список блоков, может быть либо пронумерованным, либо маркированным (по умолчанию)
    - `link` - ссылка

## Интерфейс блока CodeWizard

```ts
enum ArticleBlockType: {
    Paragraph = 'paragraph',
    Code = 'code',
    Hr = 'hr',
    List = 'list'
    Link = 'link',
}

enum ArticleColor: {
    keyWord = '0000ff',
    string = '00ff00',
    object = 'ff0000'
    // ...
}

interface ArticleBlockCommonProps {
    children: ArticleBlock[] | string;
    color?: ArticleColor;
    isBold?: boolean;
}

type ArticleBlock = ({
    type: ArticleBlockType.Paragraph | ArticleBlockType.Hr
} | {
    type: ArticleBlockType.Link;
    href: string;
} | {
    type: ArticleBlockType.Code,
    isInline?: boolean
} | {
    type: ArticleBlockType.List,
    isNumbered?: boolean;
}) & ArticleBlockCommonProps

interface ArticleAnswer {
    titleText: string;
    titleUrl: string;
    titleGreenUrl: string;
    children: ArticleBlock
}
```

## Структура данных приходящих от бекэнда

```json
{
    "docs_right": [
        {
            "data": {
                "answer": [
                    {
                        "type": "paragraph",
                        "content": [
                            {
                                "type": "code",
                                "content": ["console.log('Hello ')&NewLine;console.log('World!')"]
                            },
                            {
                                "type": "hr"
                            },
                            {
                                "type": "list",
                                "numbered": true,
                                "content": [
                                    {
                                        "type": "code",
                                        "inline": true,
                                        "content": {
                                            "type": "link",
                                            "href": "http://example.com",
                                            "content": [
                                                {
                                                    "type": "color",
                                                    "content": ["go to example.com"],
                                                    "color": "object"
                                                }
                                            ]
                                        }
                                    }
                                ]
                            }
                        ]
                    }
                ],
                "question": [
                    {
                        "type": "paragraph",
                        "content": "why?"
                    }
                ]
            }
        }
    ]
}
```

## Пример

```tsx
    <Article
        titleText="How to get selected html text with javascript?"
        titleGreenUrl="stackoverflow.com"
        titleUrl="example.com"
    >
        <ArticleBlock
            type={CodeWizardBlockType.Paragraph}
        >
            <ArticleBlock
                type={CodeWizardBlockType.Paragraph}
            >
                In IE <= 10 browsers, it's:
            </ArticleBlock>
            <ArticleBlock
                type={CodeWizardBlockType.Paragraph}
            >
                <ArticleBlock
                    type={CodeWizardBlockType.Code}
                >
                    <ArticleBlock
                        type={CodeWizardBlockType.Code}
                        isInline
                        color={ArticleColor.object}
                    >
                        document
                    </ArticleBlock>
                    selection.createRange().htmlText
                <ArticleBlock/>
            </ArticleBlock>
            <ArticleBlock
                type={CodeWizardBlockType.Paragraph}
            >
                As @DarrenMB pointed out IE11 no longer supports this. See this answer for reference.
            </ArticleBlock>
            <ArticleBlock
                type={CodeWizardBlockType.hr}
            />
            <ArticleBlock
                type={CodeWizardBlockType.Paragraph}
            >
                In non-IE browsers, I just tried playing with this... this seems to work, WILL have side effects from breaking nodes in half and creating an extra span, but it's a starting point:
            </ArticleBlock>
            {/* ... */}
        </ArticleBlock>
    </Article>
```
