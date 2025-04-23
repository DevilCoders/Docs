# Yamoney-guidelines

Библиотека блоков [Yamoney-guidelines](https://yamoney.design).

## Подключение библиотеки к проекту через npm

1. Установить библиотеку:

```bash
npm install yamoney-guidelines --save
```

2. Для БЭМ также необходимо подключить библиотеку, чтобы она попадала в сборку. Для этого, например, в файле `./enb/config/levels/desktop.js` добавить eё в массив `externalLevelsLibs`:

```js static
{
	path: 'node_modules/yamoney-guidelines/common.blocks'
}
```

## Использование библиотеки в БЭМ-проекте

Добавить в `deps.js` файл корневого блока страницы зависимость:

```js static
{
	block: 'theme',
	mods: {color: 'default', size: 'default', space: 'default'}
}
```

## Использование библиотеки в React-проекте

Импортировать и использовать в проекте:

```jsx
<Text
	align="right"
	textDecoration="underline"
	display="block"
	indent="xxxxl"
	size="l"
	letterSpacing="m"
	fontStyle="italic"
	transform="uppercase"
	type="blockquote"
	view="brand"
	weight="thin"
>
	Люк, я твой отец
</Text>
```

Для вложенных компонентов наследуется структура как в БЭМ + переопределение тем/цветов:

```jsx
<PtTable view="default" border="all">
	<PtTable.Row view="head">First row</PtTable.Row>
	<PtTable.Row border="bottom" status="error">Second row with bottom border</PtTable.Row>
	<PtTable.Row>Third Row</PtTable.Row>
	<PtTable.Row stripe="even">Fourth Row</PtTable.Row>

	<PtTable.Row spaceV="xl">
		<PtTable.Column align="right" width="50">
			Column1 with all sides padding
		</PtTable.Column>
	</PtTable.Row>
</PtTable>
```
