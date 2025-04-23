## Распределенные локи в ecstatic
У лока есть 2 дедлайна:  **till** (мягкий дедлайн, который можно продлевать) и **deadline** (жесткий дедлайн, который нельзя продлевать). Лок автоматически снимается, когда истекает любой из этих дедлайнов.

Пример: есть большая задача, которая может выполняться вплоть до часа.
Для нее имеет смысл поставить жесткий дедлайн полтора часа, а мягкий дедлайн - 5 минут и продлевать его по необходимости.

<table>
	<thead>
		<tr> <th> Запрос </th>  <th> Что получает </th>  <th> Оригинальные названия </th> <th> Зачем мне это? </th> </tr>
	</thead>
	<tbody>
		<tr>
			<td rowspan="4"> POST /locks/get </td>
	        <td> FQDN контейнера </td>
			<td> who </td>
			<td rowspan="4"> Получает лок и возвращает его <b>id<b/> </td>
		</tr>
		<tr> <td> Название лока </td> <td> name </td> </tr>
		<tr> <td> Мягкий дедлайн </td> <td> till </td></tr>
		<tr> <td> Жесткий дедлайн </td> <td> deadline </td></tr>
		<tr> <td> POST /locks/release </td> <td> Id лока </td> <td> id </td> <td> Освобождает лок с заданным <b> id <b/> </td> </tr>
		<tr>
			<td rowspan="3"> GET /locks/list </td>
	        <td> FQDN контейнера </td>
			<td> who </td>
			<td rowspan="3"> Возвращает список локов созданных не позднее <b>now - age_limit<b/>  </td>
		</tr>
		<tr> <td> Минимальный возраст лока </td> <td> age_limit{Default:0} </td> </tr>
		<tr> <td> Момент отсчета </td> <td> now{Default:now()} </td></tr>
		<tr>
			<td rowspan="2"> POST /locks/extend </td>
	        <td> Id лока </td>
			<td> id </td>
			<td rowspan="2"> Увеличивает мягкий дедлайн до заданного значения  </td>
		</tr>
		<tr> <td> Новый дедлайн </td> <td> till </td> </tr>
   </tbody>
</table>
