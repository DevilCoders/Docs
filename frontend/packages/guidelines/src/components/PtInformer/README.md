Информационный паттерн, имеющий статус. Вставляется, как в контент, так и на отдельный интерфейсный слой.

### Свойства компонента PtInformer

| Название | Значения | Описание |
| -------- | -------- | -------- |
| `view` | `default` `success`(deprecated) `alert`(deprecated) `warning`(deprecated) `system`(deprecated) | Тип отображения |
| `border` | `all` | Добавление рамок |

### Свойства компонента PtInformer.Content

| Название | Значения | Описание |
| -------- | -------- | -------- |
| `distribute` | `default` `center` `between` | Задает тип отображения потомков |
| `spaceV` | `s` `m` `l` `xl` `xxl` | Внутренние отступы по вертикали |
| `spaceH` | `s` `m` `l` `xl` `xxl` | Внутренние отступы по горизонтали |
| `spaceA` | `s` `m` `l` `xl` `xxl` | Внутренние отступы по всем сторонам |

### Свойства компонента PtInformer.Action

| Название | Значения | Описание |
| -------- | -------- | -------- |
| `align` | `center` `right` | задает тип отображения потомков |
| `spaceV` | `s` `m` `l` `xl` `xxl` | Внутренние отступы по вертикали |
| `spaceH` | `s` `m` `l` `xl` `xxl` | Внутренние отступы по горизонтали |
| `spaceA` | `s` `m` `l` `xl` `xxl` | Внутренние отступы по всем сторонам |
| `spaceB` | `s` `m` `l` `xl` `xxl` | Внутренний отступ внизу |

### Свойства компонента PtInformer.Column

| Название | Значения | Описание |
| -------- | -------- | -------- |
| `align` | `center` | Тип отображения |

```jsx
<PtInformer border='all' view='default'>
	<PtInformer.Content distribute='default'>
		<PtInformer.Column> Column-1 </PtInformer.Column>
		<PtInformer.Column> Column-2 </PtInformer.Column>
	</PtInformer.Content>
	<PtInformer.Action> Action </PtInformer.Action>
</PtInformer>
```

### Пример использование паттерна

```jsx
const {default: styled} = require('styled-components');
const Icon2 = require('../Icon2').default;
const CheckIcon = require('../Icon2/check/s').default;
const {colorYamoneyAlert, colorYamoneySuccess, colorYamoneySystem, colorYamoneyWarning} = require('../CSSVariables');

const AlertTheme = styled.div`
    ${colorYamoneyAlert}
`;
const SuccessTheme = styled.div`
    ${colorYamoneySuccess}
`;
const SystemTheme = styled.div`
    ${colorYamoneySystem}
`;
const WarningTheme = styled.div`
    ${colorYamoneyWarning}
`;

<div>
	<AlertTheme>
		<PtInformer border='all' view='default'>
			<PtInformer.Content distribute='default' spaceA='l'>
				<PtIconPlus verticalAlign='center'>
					<PtIconPlus.Icon indentR='l'>
							<Icon2 icon={CheckIcon} size='s' view='primary' />
					</PtIconPlus.Icon>
					<PtIconPlus.Block>
							<Text size='m' view='primary'>
									Спасибо за ваше обращение наши сотрудники ответят ближайшее время
							</Text>
					</PtIconPlus.Block>
				</PtIconPlus>
			</PtInformer.Content>
		</PtInformer>
	</AlertTheme>

	<SuccessTheme>
		<PtInformer border='all' view='default'>
			<PtInformer.Content distribute='default' spaceA='l'>
				<PtIconPlus verticalAlign='center'>
					<PtIconPlus.Icon indentR='l'>
							<Icon2 icon={CheckIcon} size='s' view='primary' />
					</PtIconPlus.Icon>
					<PtIconPlus.Block>
							<Text size='m' view='primary'>
									Спасибо за ваше обращение наши сотрудники ответят ближайшее время
							</Text>
					</PtIconPlus.Block>
				</PtIconPlus>
			</PtInformer.Content>
		</PtInformer>
	</SuccessTheme>

	<SystemTheme>
		<PtInformer border='all' view='default'>
			<PtInformer.Content distribute='default' spaceA='l'>
				<PtIconPlus verticalAlign='center'>
					<PtIconPlus.Icon indentR='l'>
							<Icon2 icon={CheckIcon} size='s' view='primary' />
					</PtIconPlus.Icon>
					<PtIconPlus.Block>
							<Text size='m' view='primary'>
									Спасибо за ваше обращение наши сотрудники ответят ближайшее время
							</Text>
					</PtIconPlus.Block>
				</PtIconPlus>
			</PtInformer.Content>
		</PtInformer>
	</SystemTheme>

	<WarningTheme>
		<PtInformer border='all' view='default'>
			<PtInformer.Content distribute='default' spaceA='l'>
				<PtIconPlus verticalAlign='center'>
					<PtIconPlus.Icon indentR='l'>
							<Icon2 icon={CheckIcon} size='s' view='primary' />
					</PtIconPlus.Icon>
					<PtIconPlus.Block>
							<Text size='m' view='primary'>
									Спасибо за ваше обращение наши сотрудники ответят ближайшее время
							</Text>
					</PtIconPlus.Block>
				</PtIconPlus>
			</PtInformer.Content>
		</PtInformer>
	</WarningTheme>

	<PtInformer border='all' view='default'>
		<PtInformer.Content distribute='default' spaceA='l'>
			<PtIconPlus verticalAlign='center'>
				<PtIconPlus.Icon indentR='l'>
						<Icon2 icon={CheckIcon} size='s' view='primary' />
				</PtIconPlus.Icon>
				<PtIconPlus.Block>
						<Text size='m' view='primary'>
								Спасибо за ваше обращение наши сотрудники ответят ближайшее время
						</Text>
				</PtIconPlus.Block>
			</PtIconPlus>
		</PtInformer.Content>
	</PtInformer>
</div>
```

```jsx
const {default: styled} = require('styled-components');
const {colorYamoneyAlert} = require('../CSSVariables');

const AlertTheme = styled.div`
    ${colorYamoneyAlert}
`;

<div>
	<AlertTheme>
		<PtInformer border='all' view='default'>
			<PtInformer.Content spaceA='xxl' distribute="center">
				<PtInformer.Column>
					<Decorator indentB='xs'>
						<Text size='xl' view='primary' display='block' weight='bold'>
							Нужны ваши данные
						</Text>
					</Decorator>
					<Decorator indentB='m'>
						<Text size='m' view='primary' display='block'>
							Классическая панграмма, условный, зачастую бессмысленный текст-заполнитель, вставляемый в макет страницы. Условный, зачастую бессмысленный текст-заполнитель, вставляемый в макет страницы.
						</Text>
					</Decorator>
					<Text size='s' weight='bold' view='link' display='block' transform='uppercase' letterSpacing='s'>
						Перейти в раздел
					</Text>
				</PtInformer.Column>
			</PtInformer.Content>
		</PtInformer>
	</AlertTheme>

	<PtInformer border='all' view='default'>
		<PtInformer.Content spaceA='xxl' distribute="center">
			<PtInformer.Column>
				<Decorator indentB='xs'>
					<Text size='xl' view='primary' display='block' weight='bold'>
						Нужны ваши данные
					</Text>
				</Decorator>
				<Decorator indentB='m'>
					<Text size='m' view='primary' display='block'>
						Классическая панграмма, условный, зачастую бессмысленный текст-заполнитель, вставляемый в макет страницы. Условный, зачастую бессмысленный текст-заполнитель, вставляемый в макет страницы.
					</Text>
				</Decorator>
				<Text size='s' weight='bold' view='link' display='block' transform='uppercase' letterSpacing='s'>
					Перейти в раздел
				</Text>
			</PtInformer.Column>
		</PtInformer.Content>
	</PtInformer>
</div>
```

```jsx
const {default: styled} = require('styled-components');
const {colorYamoneyAlert} = require('../CSSVariables');

const AlertTheme = styled.div`
    ${colorYamoneyAlert}
`;

<div>
	<AlertTheme>
		<PtInformer border='all' view='default'>
			<PtInformer.Content align='center' distribute='default' spaceA='xxxl'>
				<PtInformer.Column>
					<Decorator indentB='s'>
						<Text size='s' view='primary' letterSpacing='s' display='block' weight='bold' transform='uppercase'>
							Нужны ваши данные 
						</Text>
					</Decorator>
					<Text size='m' view='primary' display='block'>
						Классическая панграмма, условный, зачастую бессмысленный текст-заполнитель, вставляемый в макет страницы. Условный, зачастую бессмысленный текст-заполнитель, вставляемый в макет страницы.
					</Text>
				</PtInformer.Column>
				<PtInformer.Column>
					<Decorator indentB='s'>
						<Text size='s' view='primary' letterSpacing='s' display='block' weight='bold' transform='uppercase'>
							Нужны ваши данные 
						</Text>
					</Decorator>
					<Text size='m' view='primary' display='block'>
						Классическая панграмма, условный, зачастую бессмысленный текст-заполнитель, вставляемый в макет страницы. Условный, зачастую бессмысленный текст-заполнитель, вставляемый в макет страницы.
					</Text>
				</PtInformer.Column>
			</PtInformer.Content>
		</PtInformer>
	</AlertTheme>

	<PtInformer border='all' view='default'>
		<PtInformer.Content align='center' distribute='default' spaceA='xxxl'>
			<PtInformer.Column>
				<Decorator indentB='s'>
					<Text size='s' view='primary' letterSpacing='s' display='block' weight='bold' transform='uppercase'>
						Нужны ваши данные 
					</Text>
				</Decorator>
				<Text size='m' view='primary' display='block'>
					Классическая панграмма, условный, зачастую бессмысленный текст-заполнитель, вставляемый в макет страницы. Условный, зачастую бессмысленный текст-заполнитель, вставляемый в макет страницы.
				</Text>
			</PtInformer.Column>
			<PtInformer.Column>
				<Decorator indentB='s'>
					<Text size='s' view='primary' letterSpacing='s' display='block' weight='bold' transform='uppercase'>
						Нужны ваши данные 
					</Text>
				</Decorator>
				<Text size='m' view='primary' display='block'>
					Классическая панграмма, условный, зачастую бессмысленный текст-заполнитель, вставляемый в макет страницы. Условный, зачастую бессмысленный текст-заполнитель, вставляемый в макет страницы.
				</Text>
			</PtInformer.Column>
		</PtInformer.Content>
	</PtInformer>
</div>
```

```jsx
const {default: styled} = require('styled-components');
const {colorYamoneyAlert} = require('../CSSVariables');

const AlertTheme = styled.div`
    ${colorYamoneyAlert}
`;

<div>
	<AlertTheme>
		<PtInformer border='all' view='default'>
			<PtInformer.Content align='center' distribute='default' spaceA='xxl'>
				<PtInformer.Column align='center'>
					<Decorator indentB='s'>
						<Placeholder status='alert' size='m' view='brand'/>
					</Decorator>
					<Decorator indentB='xs'>
						<Text size='xl' view='primary' weight='bold' display='block'>
							Кошелек забокирован
						</Text>
					</Decorator>
					<Decorator indentB='xl'>
						<Text size='m' view='primary' display='block'>
							Наши сотрудники ответят ближайшее время. Наши сотрудники ответят ближайшее время. Наши сотрудники ответят ближайшее время
						</Text>
					</Decorator>
					<Text size='s' weight='bold' view='link' display='block' transform='uppercase' letterSpacing='s'>
						Перейти в раздел
					</Text>
				</PtInformer.Column>
			</PtInformer.Content>
		</PtInformer>
	</AlertTheme>
	<PtInformer border='all' view='default'>
		<PtInformer.Content align='center' distribute='default' spaceA='xxl'>
			<PtInformer.Column align='center'>
				<Decorator indentB='s'>
					<Placeholder status='alert' size='m' view='alert'/>
				</Decorator>
				<Decorator indentB='xs'>
					<Text size='xl' view='primary' weight='bold' display='block'>
						Кошелек забокирован
					</Text>
				</Decorator>
				<Decorator indentB='xl'>
					<Text size='m' view='primary' display='block'>
						Наши сотрудники ответят ближайшее время. Наши сотрудники ответят ближайшее время. Наши сотрудники ответят ближайшее время
					</Text>
				</Decorator>
				<Text size='s' weight='bold' view='link' display='block' transform='uppercase' letterSpacing='s'>
					Перейти в раздел
				</Text>
			</PtInformer.Column>
		</PtInformer.Content>
	</PtInformer>
</div>
```

```jsx
const {default: styled} = require('styled-components');
const {colorYamoneyAlert} = require('../CSSVariables');

const AlertTheme = styled.div`
    ${colorYamoneyAlert}
`;

<div>
	<AlertTheme>
		<PtInformer border='all' view='default'>
			<PtInformer.Content distribute='default' spaceH='xl' spaceT='xl' spaceB='m'>
				<PtInformer.Column align='default'>
					<Decorator indentB='xs'>
						<Text size='xl' view='primary' weight='bold' display='block'>
							Кошелек забокирован
						</Text>
					</Decorator>
					<Text size='m' view='primary' display='block'>
						Наши сотрудники ответят ближайшее время. Наши сотрудники ответят ближайшее время. Наши сотрудники ответят ближайшее время
					</Text>
				</PtInformer.Column>
			</PtInformer.Content>
			<PtInformer.Action spaceH='xl' spaceB='xl'>
				<button>Заказать звонок</button>
			</PtInformer.Action>
		</PtInformer>
	</AlertTheme>
</div>
```
